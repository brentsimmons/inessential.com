@title Making Apps Is Harder Than It Needs To Be
@pubDate 2018-05-01 13:26:10 -0700
@modDate 2018-05-01 13:41:08 -0700
With the recent talk about Electron and “Marzipan” — or maybe Amber or something, [according to Mark Gurman](https://twitter.com/markgurman/status/991369046628225025) — I’m reminded of a thing I think about kind of often: that making iOS and macOS apps is way harder than it needs to be.

For most apps (except games, I suppose), a huge percentage of the code might as well be written in a scripting language. We absolutely do _not_ need to be writing everything in Swift, Objective-C, C++, or C.

“But Brent,” you say, “what about performance?”

Consider the case where you set up an animation and then run the animation. The _system_ does that animation. Or consider Core Data — your choice of language doesn’t affect how fast it can read from SQLite. Or think of networking — it’s bound by the connection, not the speed of your code. Or think of pushing a view controller onto the current navigation view controller. Or setting up view constraints. And so on.

All this code might as well be Ruby — or, preferably, a scripting language designed for app making. (I would have liked an Objective-C-without-the-C.)

And the thing that would make it all so worthwhile is editing the code *while the app is running*. You could go all day without an explicit build step!

Sure, some of your code would still have to be written in Swift or whatever. The part that really does have to be fast. I’m a performance junkie myself, so I get this. (Evergreen’s RSS parser is fast, and I wouldn’t switch it to a scripting language.)

But _most_ of most apps (again, probably besides games, about which I know nothing) could be written using a scripting language.

PS Yes, I’m quite aware that we used to have Fix & Continue. And [WebScript](http://www.wedophones.com/Manuals/AppleComputer/WebObjects%20Getting%20Started.pdf).
