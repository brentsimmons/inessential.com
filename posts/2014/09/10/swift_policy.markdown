@title Swift Policy
@pubDate 2014-09-10 12:08:08 -0700
@modDate 2014-09-10 12:09:03 -0700
Now that Swift is at 1.0, I need to set a policy for when to use Swift code and when not to.

Swift is a peer of Objective-C and you can ship apps written (all or in part) in Swift. And I expect that the share of Swift code will grow fairly quickly.

I also expect that, once I’m good at Swift, I’ll be more productive than I am with Objective-C.

That’s a big premise to accept, and it’s not based on experience yet — I’ve written only a few hundred lines of Swift code, and slowly — but it *looks* like it’s true. There are classes of bugs that won’t compile in Swift. It has very nice things like type inference and optional chaining that cut down on the amount of code I need to write and maintain.

But this means I’ll be *less* productive as I get up to speed. There’s never a good time to be less productive, but developers are used to making this particular trade-off: adopting a new thing now has benefits later.

So my policy is this: new code will be written in Swift.

There are exceptions, though. The things Swift can’t do will have to be written in Objective-C. (Luckily these are fairly rare.)

And there has to be a time limit. I forget who proposed the 45-minute rule for CSS, where you give up and just use a damn table for your layout. I don’t want to be too quick to punt when using Swift, because it means I won’t be learning as much as I could be (and I need to become expert: that’s the point), but I also can’t let my productivity go too far from what’s normal.

I’ll give myself two hours of banging-head-on-disk, then punt. As a rough guideline. (I’m not actually going to use a stopwatch.) This number may change, but it’s important to have *some* limit as I’m doing this.

Also: I got the latest version of the Swift book and I’m re-reading it. Just because it feels right. You probably don’t need to, but I feel like I do.

I’ll also keep the known issues from the Swift release notes handy, for when I do get into a weird situation. And I’ve added the <a href="http://swifter.natecook.com">Swifter</a> site to my favorites bar, for easy lookups.
