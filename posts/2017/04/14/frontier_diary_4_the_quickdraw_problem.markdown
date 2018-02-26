@title Frontier Diary #4: The QuickDraw Problem and Where It Led Me
@pubDate 2017-04-14 13:14:20 -0700
@modDate 2017-04-14 13:17:56 -0700
In my fork of Frontier there are still over 600 deprecation warnings. A whole bunch of these are due to <a href="https://en.wikipedia.org/wiki/QuickDraw">QuickDraw</a> calls.

For those who don’t know: QuickDraw was how, in the old days, you drew things to the Mac’s screen. It was amazing for its time and pretty easy to work with. Functions included things like `MoveTo`, `LineTo`, `DrawLine`, `FrameOval`, and so on. All pretty straightforward.

These days we have Core Graphics instead, and we have higher-level things like `NSBezierPath`. QuickDraw was simpler — though yes, sure, that was partly because it did less.

<p style="text-align:center">* * *</p>

I was looking at all these deprecation warnings for QuickDraw functions and wondering how I’m ever going to get through them.

I could, after all, convert all or most of them to the equivalent Core Graphics thing. But sheesh, what a bunch of work.

And, in the end, it would still be a Carbon app, but with modern drawing.

<p style="text-align:center">* * *</p>

So I thought about it from another angle. The goal is to get to the point where it’s a 64-bit Cocoa app. All these QuickDraw calls are in the service of UI — so why not just start over with a Cocoa UI?

The app has some outlines (database browser, script editor, etc.), a basic text editor, and a handful of small dialogs. *And all of that is super-easy in Cocoa.*

Use an `NSOutlineView`, `NSTextView`, and some xibs for the dialogs, and we’re done. (Well, after *some* work, but not nearly the same amount of work as actually writing an outliner from scratch.)

In other words, instead of going from the bottom up — porting the existing source code — I decided to start from the top down.

I started a new workspace and started a new Frontier project: a Cocoa app with Swift as the default language.

Then I looked at the existing source and thought about how to organize things. I came up with this:

* Frontier — App UI
* UserTalk.framework — the language
* FrontierVerbs.framework - the standard library
* FrontierDB.framework — the object database
* FrontierCore.framework — common utility functions and extensions

I like using frameworks, because it helps enforce separation, and it helps in doing unit testing. And frameworks are so easy with Swift these days.

Hardly any of this is filled-in yet. I’ve got the barest start on FrontierVerbs. [Ted Howard](https://twitter.com/tedchoward), my partner in all this, is taking UserTalk.framework and FrontierDB.framework.

In the end, it’s possible that no code from the original code base survives. Which is totally fine. But it also means that this is no quick project.

At this point I should probably put it up on GitHub, since it’s easier to write about it if I can link to the code. I’ll do that soon, possibly on the weekend.
