@title On the benefits of thin-server RSS syncing
@pubDate Tue Feb 09 15:01:19 -0800 2010
@modDate Tue Feb 09 15:16:03 -0800 2010
I’ve had a bunch of people ask me about the <a href="http://inessential.com/2010/02/08/idea_for_alternative_rss_syncing_system">thin-server RSS syncing system</a> I talked about yesterday.

The main question: what are the benefits?

First let’s define things a little. A thick-server RSS syncing system is something like Google Reader, NewsGator, Bloglines — where the server actually downloads the feeds, and client apps talk to the server rather than to the original sources.

There are lots of benefits to this kind of system. There’s every reason for this to be widely used — it’s the right choice for lots of people, probably for most.

A thin-server syncing system doesn’t read the feeds: it only knows about users, subscriptions lists, and the status of news items. No actual feed content. Loosely coupled to the actual RSS readers.

Here are some of the benefits of a hypothetical thin-server system (in no particular order):

#### No latency

The thick-server systems have to read millions of feeds. So they don’t usually get updates the moment they happen — they check a feed once an hour or whatever. (Maybe it’s every 15 minutes or whatever for popular feeds.)

This means that news gets to the client apps a little less quickly than it would otherwise.

With the thin-server, the clients read the feeds directly, so they get exactly what’s available at that time.

#### Security

Say you read a password-protected feed. A thick-server system would have to support that, *and* you’d have to send your credentials to that system. That system would have to store the content: it would treat it like any other feed it reads.

It’s not economical for thick-server systems to handle password-protected feeds, since each one can’t be re-used. It’s one copy per username/password pair.

With a thin-server system, you never transmit your username and password. It never sees the feed data, just the URL of the feed and IDs of news items. No problem syncing password-protected feeds.

#### Reachability

Say you read feeds from a local intranet that a thick-server can’t reach. You can’t sync these, since the thick server can’t read the feeds.

But, again, a thin server doesn’t care. All it sees are feed URLs and IDs of news items. No problem syncing intranet-only feeds.

(This also applies to things like script subscriptions. A thick server isn’t going to run an AppleScript, for example, but multiple clients might run the same script. The news items status would still be syncable.) (But not the script! No way would I want to sync executable code.)

#### Server downtime doesn’t prevent you from getting your feeds

If a thick-server system goes down, you can’t get your feeds. (Unless you turn off syncing.)

With a thin-server system, you still get your feeds. The clients wait to sync up.

#### Decentralized

So far, all the thick-server systems are on one big (conceptual) server. This means one point of failure for everyone who uses that system. Downtime is a big issue.

It’s conceivable that you could write a thick-server system that can run anywhere. Something open source, something easy to install. But it would use so much resources and bandwidth (reading the feeds every hour, returning entire feeds to client apps) that it would be prohibitive for many people. You couldn’t just install it on your account at your web provider and hope to get away with it. (Well, depending on lots of factors, of course. If it was just for you, and you didn’t have too many feeds, it’s probably okay.)

A thin-server system, on the other hand, would be easy to run. Minimal bandwidth, no content system where it downloads and stores feeds. It should be easier to set up and run than WordPress.

#### Easier to move from synced to non-synced and back

The thick-server systems rewrite the feeds, and usually substitute their own unique ID for whatever was in the feed. (Though, in the case of Google Reader, it also provides the original unique ID, if there was one.)

Because the feeds are rewritten, it can be very difficult to match up a non-synced item with its synced equivalent. This can make turning on or off syncing very rough, as you end up with duplicates.

#### Longer limits on news item status

This isn’t inherent, but it’s practical. Thick-server systems tend to serve a ton of people, so they have to have limits on the length of time news items status data will be stored.

For instance, NewsGator’s was two weeks or 200 items, whichever was first. (If I recall correctly.) Google Reader’s is, I believe, roughly twice that (but with some special cases, like when you do a mark-all-read in Google Reader and when you first subscribe to a feed).

But a thin system can afford to keep news item status data longer. Make it six months or a year.

#### No data loss

Because thick-server systems rewrite the feeds, they’ll often toss out parts of the original feed that they don’t care about. 

Again, this doesn’t have to be inherent, but for practical reasons it’s often done this way.

With the thin server, you read the feeds directly, so you miss nothing.

#### Twitter and other feed-like things

This system would work for anything feed-like: it just needs a URL and individual item IDs.

Imagine pointing not just your RSS readers but also your Twitter clients at the server — your Twitter clients could know which items you’ve already read. Want that? I do. :)

#### Your data in your control

You could use someone else’s server, if they allowed it. Maybe there’d be inexpensive for-pay services.

But, at least conceptually, you could run it yourself, and control all your data yourself. The opportunity would be there, at any rate.

#### Anyway

That’s all I have in my head at the moment. There are more benefits, surely, but I think the above is plenty.
