@title How Release Day Went
@pubDate 2019-08-27 13:28:27 -0700
@modDate 2019-08-27 13:28:27 -0700
Yesterday was a great day! A few things to note, in no particular order:

NetNewsWire got some press coverage, including a well-done [review in MacStories](https://www.macstories.net/reviews/netnewswire-review-the-mac-rss-client-rebooted-with-a-solid-foundation-for-the-future/).

We got a lot of feature requests, but no bug reports.

Except that we did get a single-digit number of crash logs. On investigation, I found two distinct backtraces — we’ll need to fix those. The thing is, there’s *no freakin’ way* the app should crash in those spots. Except that, obviously, it can. Rarely, but it happens.

The servers started timing-out at one point during the day. I contacted DreamHost support and they fixed things (and told me that the fixes they applied should prevent this in the future).

There were a number of nice blog posts and tweets about NetNewsWire, which was *awesome*. After working so hard for so long, it’s great when people appreciate the app. We don’t get paid in money, after all. 🐣

I have no idea how many downloads of the app there were. GitHub is hosting the download, via its releases feature, and I don’t see a way to find out how many times it’s been downloaded. Which is totally fine with me.

<p style="text-align:center">* * *</p>

I should say something more about the no-bug-reports. There’s no special magic or talent or anything to this — there’s just the willingness to say that we’re not going to ship until we’ve got the bugs out, and then sticking to that.

This is a matter of pride and ethics, for sure, but there’s another dimension: since the app is open source, it’s written by volunteers (including me), and we have no dedicated support team. Any time we spend fielding bug reports is time taken away from working on the next feature.

Making apps — even, or especially, free apps — is an exercise in economics. With free apps, the economics are even more constrained, because nobody is going to hire even a part-time support person. So we do everything we can do keep costs down — especially time costs.

Plus — buggy apps can be demoralizing to the people who work on them. Part of my job is to make sure people are proud and happy to work on the app. And that means making sure everyone knows we’re super-serious about doing our best to never ship bugs.
