@title Matthew on Twitter Restrictions
@pubDate Fri Jun 29 19:52:04 -0700 2012
@modDate Fri Jun 29 19:52:04 -0700 2012
<a href="http://thenextweb.com/twitter/2012/06/30/developers-bracing-themselves-for-twitter-api-retrictions-call-todays-post-ominous/">Matthew Panzarino</a>:

>I polled a few high-profile developers who use the Twitter platform and APIs and the general consensus was that the wording of the post was “ominous.”

I’m glad I don’t have a stake in this. But it does nudge me ever closer to quitting Twitter. (I’ve already quit Facebook, LinkedIn, and Instagram.)

#### What I’d Do

Were I a Twitter client developer, I would get in touch with other client developers and start talking about a way to do what Twitter does but that doesn’t require Twitter itself (or any specific company or service).

Once we came to a consensus, then we’d add support for whatever-it-is to our apps. We wouldn’t drop Twitter support — we’d just add the new thing. Do both.

And then we’d promote the new thing, encourage people to use it, help it grow. Then drop Twitter some day — or wait till Twitter cuts off our apps. Whatever. And not care, because we’ve got the new thing.

#### Technical Details

The interesting (to geeks like us) part is this: what system that works like Twitter could exist without a company behind it?

Think about it this way:

Under the hood, following somebody is really just subscribing to a feed of their statuses. Posting is really just updating a feed of your own statuses.

So you standardize on a feed format. RSS would work great, of course, and there’s a ton of RSS reading and writing code out there already — and it’s <a href="http://inessential.com/2011/06/15/what_we_talk_about_when_we_talk_about_rs">not like it’s dead</a>. (For instance, just this week Apple released a major <a href="http://arstechnica.com/apple/2012/06/bye-bye-downloads-apples-new-podcasts-app-enables-streaming/">iPhone app that uses RSS</a>.)

Any given feed could live anywhere on the web.

It’s one feed per “account” — with “account” in quotes because there are no actual accounts anywhere.

Each feed would need an associated file that lists the people that that person follows. Under the hood this is just like an RSS subscription list — and <a href="http://dev.opml.org/">OPML</a> makes sense for this file.

Do this much, and you’ve got the basics down: following, reading, and posting.

For searching and mentions, a client could just look at the feeds it’s already reading — but for system-wide searching and mentions some special services would need to be built (is my guess). But there could be many competing services instead of just one indispensable service. (For instance, years ago there used to be services that specialized in blog-searching. This would be similar.)

(Same for direct messages, though I think that might be one Twitter feature that you don’t really need. People already have ways of contacting each other privately — email, SMS, chat — so time spent on this might be a waste of time.)

#### Side Effect: Stuff to Read Is Already Available

If you did the above, and chose RSS as your format, you’d also have the ability to “follow” Daring Fireball, Macworld, The Next Web, Apple — every site that has a feed. Your UI might truncate the posts to make them more tweet-like, of course — but it means you’ve already got a ton of content for people to follow.

Think of how there’s an <a href="http://twitter.com/daringfireball">@daringfireball</a> Twitter account — in this system you’d just use its RSS feed instead.

#### Nobody Could Shut You Down

Some people are committed to using the open web versus APIs from other companies. Some people don’t care.

But there’s a practical reason to use the open web: your app <em>can’t</em> be shut down. And Twitter is looking more and more like a company that’s thinking about shutting apps down.
