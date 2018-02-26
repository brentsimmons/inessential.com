@title Secret Projects Diary #2: Swift 2.0 Protocols
@pubDate 2015-07-19 11:08:26 -0700
@modDate 2015-07-19 11:28:38 -0700
Let’s say I’m writing an RSS reader. (This is the example I tend to use on my blog, for historical reasons, and shouldn’t be taken as indicative of anything.)

Let’s say the RSS reader can have a mix of stand-alone feeds and feeds that are synced with FeedBin, Feedly, NewsBlur, etc. I might very well do this:

* Create a Feed protocol.
* Create classes for each different type of feed: LocalFeed, FeedBinFeed, FeedlyFeed, etc. Each one of these conforms to the Feed protocol.

(Why? Because each syncing system is different, and rather than have a giant Feed class that can handle all the different types, it’s smarter to have a Feed protocol and then specific implementations for each different type of feed.)

RSS readers tend to have folders too. But folders may have different rules, depending on the system: folders inside folders may or may not be allowed, for instance. So, similarly, I might do this:

* Create a Folder protocol.
* Create classes for each different type of folder: LocalFolder, FeedBinFolder, FeedlyFolder, etc. Each one of these conforms to the Folder protocol.

The Folder protocol includes the following:

<code>var feeds: [Feed] {get}</code><br />
<code>func addFeeds(feedsToAdd: [Feed])</code>

Now, in a concrete implementation of `addFeeds`, I want to check that each feed isn’t already contained in the folder.

<code>func addFeeds(feedsToAdd: [Feed]) {</code><br />
<code>&nbsp;&nbsp;for oneFeed in feedsToAdd</code><br />
<code>&nbsp;&nbsp;&nbsp;&nbsp;if !feeds.contains(oneFeed) {</code><br />
<code>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;feeds += [oneFeed]</code><br />
<code>&nbsp;&nbsp;}</code><br />
<code>}</code>

But I can’t: I get <code>Cannot invoke 'contains' with an argument list of type '(Feed)'</code>.

Okay, I think — let’s just use a Set anyway. Probably should have been a Set all along.

So I change the Folder protocol to make feeds a set:

<code>var feeds: Set&lt;Feed> {get}</code>

And on that line I get an error: <code>Type 'Feed' does not conform to protocol 'Hashable'</code>.

So I try to make the Feed protocol Equatable, and I can’t. (And it has to be Equatable to be Hashable.)

<p style="text-align:center">* * *</p>

I believe in protocol-based programming. Big, big fan. But it’s here where I get frustrated.

It occurs to me that I’m still new to Swift, and I’m trying to use Objective-C patterns. That’s fair and true.

The Objective-C version of all of this is pretty natural, though. Given Feed and Folder protocols, I can do this:

<code>- (void)addFeeds:(NSArray \*feedsToAdd) {</code><br />
<code>&nbsp;&nbsp;NSMutableArray \*feedsArray = [self.feeds mutableCopy];</code><br />
<code>&nbsp;&nbsp;for (id&lt;Feed> oneFeed in feedsToAdd) {</code><br />
<code>&nbsp;&nbsp;&nbsp;&nbsp;if (![feedsArray containsObject:oneFeed]) {</code><br />
<code>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[feedsArray addObject:oneFeed];</code><br />
<code>&nbsp;&nbsp;&nbsp;&nbsp;}</code><br />
<code>&nbsp;&nbsp;}</code><br />
<code>&nbsp;&nbsp;self.feeds = [feedsArray copy];</code><br />
<code>}</code>

(A version where self.feeds is an NSSet is even simpler.)

It occurs to me that there probably *is* an answer in Swift. But it probably means more code. Objective-C syntax may be more verbose, but the fact that I can treat <code>id&lt;Feed></code> as an object without having to stand on my head is important because, again, I’m a huge fan of protocol-based programming. (And I’m a huge fan of less code.)

Let’s just say that I’m doing it wrong. What’s the right way to do this?

<p style="text-align:center">* * *</p>

Aside:

“Brent — if you love Objective-C so much, why don’t you marry it?”

Here’s the deal: I’m 47 years old, and if I start ignoring new things, I’ll fall behind and won’t be able to catch up. When you’re 30 or even 40 you can safely ignore things for a while and catch up later. Later on it’s harder and time is shorter. So I’m learning Swift.

And, by the way, I’m *enjoying* it. There’s so much to love. But sometimes I hit roadblocks and Swift’s type system feels like a straightjacket — and then I miss the elegance of my beloved Smalltalk-derived Objective-C.

<p style="text-align:center">* * *</p>

<b>Update 11:25 am</b>: I created a playground showing my conundrum: <a href="http://ranchero.com/downloads/RSSReaderExample.playground.zip">RSSReaderExample.playground.zip</a>. (May require Xcode 7 beta.)
