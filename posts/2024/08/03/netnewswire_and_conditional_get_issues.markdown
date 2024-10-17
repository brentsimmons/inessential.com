@title NetNewsWire and Conditional GET Issues
@pubDate 2024-08-03 14:21:37 -0700
@modDate 2024-08-03 14:37:09 -0700
I had thought that NetNewsWire’s conditional GET support was rock-solid — and so my first reaction was to be very surprised to [learn that it’s not](https://rachelbythebay.com/w/2024/08/02/fs/)!

My second reaction was to be appreciative — Rachel’s work here on setting up a test server and reporting on the results is really great. My goal has always been to make NetNewsWire a model net citizen, and learning where it’s not is super valuable. So: much respect and thanks to Rachel for this.

#### The Data

Let’s look at some data and try to figure out what’s happening. [Here’s Rachel’s report for NetNewsWire](https://rachelbythebay.com/api/fsr/4467c09c31370b8375c6b2a320aa77cd5d999cd4).

Things to know: these are all requests for a NetNewsWire-specific feed, and the copy of NetNewsWire making these requests is on my personal laptop. That laptop is occasionally used for development, which can throw things off, but not often. You can even see in the data a gap lasting just over two weeks where there were no requests (I was on vacation).

(You can also see some anomalies from when I had it on my dev machine also — ignore every row where ip is v6, since that’s my dev machine.)

Another thing to know: this is testing direct feed-reading, as with the On My Mac (or iPhone/iPad) and iCloud accounts. With systems such as Feedly, Feedbin, and so on, we get the data from the sync system and not directly from the site.

#### Ignoring Timing Issues

Let’s set aside, at least for today, the timing issues. That situation could be improved, but it very much reflects that this is a desktop app with a command that allows you to refresh feeds manually, without having to wait for the next poll.

#### Conditional GET Issues

First, a refresher on how this should work.

When a server returns a Last-Modified header, the client should return that exact same string in follow-up requests in an If-Modified-Since header. The server then looks at the If-Modified-Since header and decides to either return a 200 plus the feed — if it *has* been modified since — or return a 304 Not Modified response and an empty body.

It’s the same story with the Etag header. The client should save it and return it in follow-up requests in an If-None-Match header.

This is great because it can save a ton of bandwidth, which is great for server and app alike. And NetNewsWire’s been doing this since the early 2000s.

But clearly there’s a bug! In some cases, NetNewsWire is not picking up and saving the changed Last-Modified and Etag headers. Sometimes it does, and sometimes it keeps using whatever it already had and ignores the new ones.

What could account for this? Let’s look at the logic.

#### Feed processing logic

Here’s what happens when a feed download completes without errors and the content is non-empty:

First we check the hash of the raw feed data against the hash of the raw feed data the last time it actually changed. If those hashes match, then the app stops processing, because the feed hasn’t changed: it’s exactly the same as last time.

This is an optimization that deals with the fact that many servers unfortunately don’t support conditional GET. It allows the app to skip feed parsing and updating the database. Saves a bunch of work. Good for battery life.

If the hashes don’t match, then processing continues: it parses the feed and then sends the parsed articles to the code that updates the database.

After that it updates and saves the hash of the raw feed data, and finally it stores the conditional GET info — it saves any Last-Modified and Etag header values to send with the next request.

This isn’t actually the code, but it’s what the logic looks like:

	downloadDidComplete(httpResponse, feed, feedData)
		hash = feedData.md5
		if hash == feed.previousHash then return
		parsedFeed = parse(feedData)
		updateDatabase(feed, parsedFeed)
		feed.previousHash = hash
		feed.conditionalGetInfo = conditionalGetInfoFromResponse(httpResponse)

#### My theory

There’s a great chance you’ve already spotted what I think is the issue: it’s that optimization where we check the hash of the raw feed data and return if it matches the previous hash.

Here’s what I think has happened in some of the tests: the raw feed data was unchanged, but one or both of the Last-Modified and Etag header values *did* change.

NetNewsWire never picked up the changes to those headers, because that code didn’t run — it had already bailed when it saw that the raw feed data was unchanged.

The assumption I made when I wrote this code was that if the raw feed data was unchanged then of course the Last-Modified and Etag header values would be unchanged too, so there was no need to check to see if they were new.

And I think that in real-world situations this is probably true pretty much all the time, and it’s only in tests like this where my assumption wouldn’t be true.

But I can’t say that for sure! This is a real bug, and we’ll fix it and add a test or tests to make sure it doesn’t happen again.

Here’s what the new logic should look like:

	downloadDidComplete(httpResponse, feedData, feed)
		hash = feedData.md5
		if hash != feed.previousHash {
			parsedFeed = parse(feedData)
			updateDatabase(feed, parsedFeed)
			feed.previousHash = hash
		}
		feed.conditionalGetInfo = conditionalGetInfoFromResponse(httpResponse)

With the above logic, conditionalGetInfo gets updated no matter what.

#### PS There could be other bugs

My theory does point to a bug that should get fixed. But is it the only bug? Is it even the bug that causes the issues in these tests?

Though I’m pretty confident that this is the bug — seems pretty obvious, right? — more investigation and testing is warranted.
