@title Idea for alternative RSS syncing system
@pubDate Mon Feb 08 22:18:32 -0800 2010
@modDate Mon Feb 08 22:18:32 -0800 2010
Google Reader is an RSS reader that can be used for RSS syncing. Bloglines used to have a very basic syncing API (maybe it still does). NewsGator had a syncing API. FeedSync is a way to use feeds to sync other stuff (as far as I can tell). Sync Services (MobileMe syncing API) is a generalized syncing system that might be able to do RSS, but works just between Macs.

WebDAV is cool. DropBox is super-amazingly-cool. But these are storage systems, not syncing systems for things like RSS.

Not one of the above is a really great system for <em>just syncing</em> RSS between apps.

(For people who remember NewsGator’s system with fondness: it had drawbacks too, including that it was limited to the past two weeks or 200 items for each feed.)

Now, that said, I think Google Reader is cool (both as app and API), and I’m very glad we can use it, and I totally appreciate the help we’ve had from Google. But I do also hear from NetNewsWire users who’d like an alternative.

With everything else I have to do, I don’t have time to create an alternative. But I could make NetNewsWire work with an alternative, if one existed and was worthwhile.

#### What is a worthwhile alternative?

There are a few criteria to meet, in no particular order:

1. It would have to be more like email servers — that is, not just one big server or cluster of servers somewhere, but the kind of thing people can run on any server. My web service provider might run one for me, the same way it runs an email server. (Or I might run one on my LAN. Or I might install it myself on my own website.)

2. It would have to be free and open source, so that it could be everywhere, so that it would be developed by people who just want to make RSS syncing work. (I’m a capitalist, totally, but there are times when free and open source makes sense.)

3. It would have to work over http and https. REST API.

4. It would have to *not* require that clients download the feeds themselves from the server. (This is the way Google Reader, NewsGator, Bloglines and others worked. Status info was added to the rewritten feeds. I’m saying this system should *not* work that way: clients would download feeds directly from their sources, just as they do when not syncing.)

5. The API should be as simple as possible and still get the job done. The job would be defined as syncing subscriptions lists and status of individual news items in RSS and Atom feeds. (And nothing else!)

6. It would have to be easy to configure an RSS reader to use a given server. No more than URL of server, username, and password should be required. (Less, if possible.)

7. It should not be limited to the last 14 or 30 days (like some systems) — it should have a much larger limit, like a year.

8. The server itself wouldn’t ever read any RSS feeds. It wouldn’t have to — it’s entirely just about syncing data between apps. It would only ever talk to client apps.

9. It should use as little bandwidth as possible, and be as fast as possible.

10. Authentication would use standard HTTP authentication. (Not cookies or anything else.)

11. There should probably a PHP + MySQL version, just so it can be deployed as widely as possible. (Though I know you’re thinking Rails.)

12. Despite its being open source, if someone did want to offer it as a for-pay service, they should be allowed to.

#### Notes about the API

There are some obvious things. Get subscriptions list as OPML-with-folders. (Feeds could live in multiple folders, which means folders are just like tags, so call them tags if you want to.)

API calls would support conditional GET, so getting a subscription list would usually result in a 304.

You’d probably add, delete, edit subscriptions by addressing into the tree. (That way you could delete one instance of a feed that appears multiple times. You could add/remove folders that way too.)

The other half is the status of news items. Most have a unique ID (always in the case of Atom) or a guid (usually, in the case of RSS). For items that don’t, an agreed-upon way of constructing a unique ID would have to be developed. (Pick things that don’t usually change but are enough to identify an item: pubDate in a specific format + link + feed URL, as a UTF-8 string, then MD5-hashed. Maybe. Something like that, something that would be largely reliable.)

You’d sync status incrementally: get all the status changes since a certain date (the last time you made the call). Status would probably be read, unread, deleted, starred, and saved. To set status, it would be great to address each item in individual calls, very RESTfully — but that would be a giant bandwidth waste. Better a single call that takes a structure of some kind (XML, JSON, whatever) with item IDs and status/value pairs, where you can update a bunch of items all at once.

As you can see, the server doesn’t have to do that much. It stores some small bits of data with timestamps. I don’t think it needs any cron jobs (at least not conceptually) — it just responds to requests. It doesn’t even have any idea what this data is about.

You probably have the database schema mapped out in your head already plus more specific ideas about the API. 

(I don’t recall if I’ve said before, but a couple years ago we found that the average NetNewsWire user had 26 subscriptions. That should give you an idea of the storage requirements this would need. Obviously some people have hundreds or thousands, of course, but not most.)

Most of the time clients are just getting the subs list (usually getting a 304 back), and getting/setting news item status changes.

In other words, none of this sounds that hard. And it doesn’t sound like a taxing job for a server.

#### Invitation

If I had time, I would have written this years ago, offered it for free, made it open source, had NetNewsWire support it, and I’d have tried to get other RSS readers to support it too.

But I didn’t and don’t have time to write it.

However, if there are people who are interested in writing this, I can help. I have client apps, and I’ve been thinking about this for years, and I’ve written to several sync APIs.

If you’re seriously interested in writing some software that could end up deployed far and wide, and that would solve a real problem for real people, get in touch with me.

#### P.S. Here’s the business case

So you might want to make some money. That’s cool. Two business ideas:

1. Charge people money to use the service.

2. Collect information about popular feeds and popular news items. You could provide a real-time view into what people (in the aggregate) are reading. This might be interesting to sell, or it might be interesting as a website itself (where you could display ads). Given all the metadata in feeds, plus your user’s folders/tags, you might even be able to figure out categorization. You might even be able to provide trends, too. Certain topics are gaining/losing ground. Certain feeds are getting more or less popular. Etc. Don’t forget the pretty graphs! All of that stuff would be an add-on, of course, something you’d be able to build because you have the sync system underneath.

Compelling? I don’t know. Just what I thought of off the top of my head.
