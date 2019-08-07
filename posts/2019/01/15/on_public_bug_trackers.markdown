@title On Public Bug Trackers
@pubDate 2019-01-15 13:41:24 -0800
@modDate 2019-01-15 13:44:14 -0800
For open source projects it makes sense to have a public bug tracker. It would be hard to do the work without it.

But for commercial software? It’s not a good idea at all.

(I bring this up because I saw someone suggest this idea recently, and it stuck in my head.)

Decisions about what to work on — and when, and by whom — are *complicated*. From the outside it might look like it’s as simple as picking the next feature request with the most votes, but it’s not that simple.

A company might prioritize a crashing bug over that bug.

Or that feature might need x, y, z and done first, all of which require major work — maybe it needs some surprising amount of design or under-the-hood work, or both, that the requestors understandably don’t know about. Or it needs a bunch of localizations. Or lots of extra testing because the implementation is complex or wide-ranging — or it’s in an area where it could cause regressions.

Or the person who best knows that area of the code is temporarily on another team to help with another company priority. Or that person is going on vacation.

Or there are features nobody has asked for specifically, but that the company thinks would be awesome, and those get priority.

Or there are a half-dozen features that are low-hanging fruit, and for various reasons it’s a good idea to do a bunch of easy things for a while.

Or the feature doesn’t even really *fit* with the app: companies make that call all the time. (I never added Usenet support to NetNewsWire, despite getting requests for it.)

Or the feature is actually impossible. Or impossible without spending two years and a few million dollars on research and development first.

Or there’s a new OS feature that should be supported. Or an incompatibility with a new OS to fix.

And so on — the list goes on.

But if you have a public bug tracker, you’d likely find that you’re having to explain your decisions all the time. You’d be constantly defending your plans to people who remind you that Feature X has all these votes, so why hasn’t it shipped yet?

I’d argue that most companies aren’t open and accessible enough. Many companies don’t listen to their users very well. Many don’t even write honest and respectful release notes.

But opening up the bug tracker to the public is just a way to get bogged down: it’s a way to make worse decisions, and make them more slowly.
