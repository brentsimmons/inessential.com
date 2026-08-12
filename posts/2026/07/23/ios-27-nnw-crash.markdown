@title New NetNewsWire Crash in iOS 27 Beta Has Made Me a Bit Salty
@pubDate 2026-07-23 10:52:45 -0700

I returned from a lovely summer vacation (family, beach) to find that iOS 27 beta has fucked up the transition between split view and compact — I’ve got a boatload of crashes, mostly on Pro Max devices and a few on iPad.

Here’s a [representative crash log](https://github.com/Ranchero-Software/NetNewsWire/issues/5371). The feedback in TestFlight all talks about rotating the phone.

Here’s the thing: iOS app development (and Mac, but to a lesser extent) is just constant churn. I thought I was getting a year off this year! But nope. There’s always something.

My theory is that the automatic split view collapsing, which NetNewsWire uses, is just no longer an option, and I’ll have to specify a separate compact view controller.

So that’s just a bunch more work and testing, including testing on previous iOS versions (we go back to iOS 17), and *not* improvements like performance enhancements and new features. It’s just treading water. It’s a waste of time. For what reason? Why?

**Update the next day (24 July 2026):** This bug appears to be have been fixed by Apple in [iOS 27 beta 4 build 24A5390f](https://betawiki.net/wiki/IOS_27.0_build_24A5390f), released July 20, before my report here. I can confirm that I’ve not seen this crash in this new build.

Thank you to the team that prioritized and fixed this!
