@title Vesper Mac Diary #4 - Reporting Bugs
@pubDate 2014-06-29 21:41:45 -0700
@modDate 2014-06-29 21:43:04 -0700
Last summer I worked on Vesper for iOS 7 using the iOS 7 betas. And I was busy, and we had a deadline (iOS 7’s ship date, which we probably didn’t actually know precisely) — and I didn’t bother to report bugs until after iOS 7 shipped.

Which was a mistake.

In fact, my attitude with other iOS and OS X releases has always been to wait and get a near-finished beta and deal with whatever needs dealing with. That works fine most of the time.

But last year I could have reported some important bugs which might — might — have been fixed in time for the iOS 7 release. Or perhaps they’d have been fixed in a subsequent update.

While I’m not responsible for another company’s bugs, I *have* changed my attitude about this. It doesn’t matter how busy I am, I’m going to report everything I notice, whether small or large.

And the reason is self-serving: the bugs I find are the bugs that affect my apps, and I dearly want those bugs not to exist. If the only way I can help is to report bugs, then I’ll report bugs.

I’ve reported a few today. Here’s another one with a sample project: <a href="http://ranchero.com/downloads/ToolbarSpacer.zip">ToolbarSpacer.zip</a>. Toolbar items that are single-segment NSSegmentedControl objects get extra space to the right. Note that the label isn’t centered, and clicking on the apparently blank space doesn’t move the window. (Xcode 6 beta 2. Latest 10.10.) (<a href="rdar://17501552">rdar://17501552</a>.)
