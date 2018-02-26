@title What I’m Doing With These Articles
@pubDate 2016-05-18 19:22:49 -0700
@modDate 2016-05-18 19:22:49 -0700
In case it’s not clear: with recent and future articles I’m documenting problems that Mac and iOS developers solve using the dynamic features of the Objective-C runtime.

My point isn’t to argue that Swift itself should have similar features — I think it should, but that’s not the point.

The point is that these problems will need solving in a possible future world without the Objective-C runtime. These kinds of problems should be considered *as that world is being designed*. The answers don’t have to be the same answers as Objective-C — but they need to be good answers, better than (for instance) writing a script to generate some code.

(Swift is just one part of that future world. The part I care about more, *far* more — as much as I love Swift — is any app frameworks built on Swift. But the design of Swift has an impact on the design of those frameworks.)

There’s a second point: many people writing in Swift right now seem not to realize the extent of their reliance on Objective-C’s dynamism. Even if you don’t write a line of Objective-C, you’re running a ton of code that *is* Objective-C, and that dynamic runtime, and the app frameworks built on top, is what makes your apps actually work. This is kind of a “duh” thing, I realize, but it’s worth the reminder.

Next up (probably Thursday or Friday) will be a thing on easily updating local model objects with data downloaded from a server. And then more to come.
