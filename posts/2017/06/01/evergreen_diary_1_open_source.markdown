@title Evergreen Diary #1: Open Source
@pubDate 2017-06-01 17:27:32 -0700
@modDate 2017-06-01 17:37:08 -0700
<a href="https://ranchero.com/evergreen/">Evergreen</a> is a new feed reader for Macs. It’s not actually *done* yet — in fact, it’s not even alpha yet, much less beta. It’s still in the painful-to-use stage, for sure.

I’ve been working on it (<a href="http://inessential.com/frontierdiary">among other things</a>) on nights and weekends for a couple years. For much of the time I planned to make it a for-pay app — the plan was a free Lite version and a for-pay version.

But as time went on I was less and less motivated to make a for-pay app. Doing all that stuff — dealing with licenses, money, a store, support, and everything else that goes along with a commercial app — just didn’t sound like any fun, and it would have taken time away from actually working on the app, which is all I really want to do. I just don’t have time to spare.

So I decided to make it free and open source. (The <a href="https://github.com/brentsimmons/Evergreen">code is up on GitHub</a>.) This fits with my goals:

* Promoting feed-reading as part of promoting the open web.
* Publishing a bunch of feed-reading code and an example Mac app that other developers can use.
* Giving me something to write about on this blog.

I like developing in public. Publishing the code makes it feel like a performance, a kind of <a href="https://www.youtube.com/watch?v=d2Z9qN8R9Bg">tightwire act</a>. Which suits me.

<p style="text-align:center">* * *</p>

The one thing that almost held me back from making it open source was the effect on other developers. There are for-pay Mac feed readers, after all, and I don’t want to take anything away from them.

And I don’t want to send the message that software ought to cost nothing.

I think that making it open source makes it an obvious special case. There is at least <a href="https://github.com/ViennaRSS/vienna-rss">one other open source Mac feed reader</a>, and there are other open source Mac apps, and I don’t think that these projects are fueling the race to the bottom with app pricing.

I went over and over this decision for months. It wasn’t easy! But in the end I decided it’s a good thing, and there are always good reasons not to do a good thing.
 
<p style="text-align:center">* * *</p>

The app doesn’t have any icons yet. [Brad Ellis](https://twitter.com/BradEllis), who I’ve worked with before on some versions of my previous feed reader, and who is my favorite designer, is working on icons.

Brad is not only my favorite designer, he’s the favorite designer of people who thought they might be my favorite designer. :)

<p style="text-align:center">* * *</p>

At some point it will sync with some existing systems (such as <a href="https://feedly.com/">Feedly</a>, <a href="https://feedbin.com/">FeedBin</a>, and similar) — but probably not till after 1.0, though as top priority.

I have no plans to make an iOS version (though anything could happen). The plan is to make it a great Mac app. Period. But if it syncs with Feedly and so on, then you could use some other reader on iOS and it would sync with Evergreen.

<p style="text-align:center">* * *</p>

There is a road not taken here that’s worth exploring, though probably not by me (for reasons of time).

I would love to see a casual feed reader (as opposed to productivity-style) that just provides a timeline, with new stuff at the top. The idea is to make something like a Twitter client but for feeds. You’d get a list of articles, and when you want to read something you’d click (or whatever) to open the article in your browser.

Such an app wouldn’t have per-article read/unread status — instead it would maintain a high-water mark, the date of the newest item you’ve seen in the timeline.

For a little while I was planning to do *both* styles of reader, since so much of the code would be shared. But that was overly ambitious, so I dropped the idea.

But *you* could do it.

<p style="text-align:center">* * *</p>

I made a Twitter account: <a href="https://twitter.com/evergreen_mac">evergreen_mac</a>. Though I have no fondness for Twitter, it seems like app makers need to be accessible that way. Most Evergreen users will probably be on Twitter.

But you don’t have to use it: you can <a href="https://github.com/brentsimmons/Evergreen/issues">report bugs and make feature requests</a> via GitHub. And that way they’re in the system, which is good.

You can also email me: I’m brent at the domain name that appears in the link that starts the first sentence of this post.
