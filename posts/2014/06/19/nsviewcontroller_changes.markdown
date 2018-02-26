@title NSViewController Changes
@pubDate 2014-06-19 12:07:18 -0700
@modDate 2014-06-19 12:07:18 -0700
iOS developers outnumber Mac developers, surely, and I wouldn’t be surprised if it’s more than one order of magnitude.

That should change. iOS developers ought to know that writing Mac software is fun, and Mac apps can make real money.

One of the unsung, or not-sung-enough, set of changes announced at the recent WWDC is a change to how view controllers work on Macs.

Starting with Yosemite:

* Storyboards are supported on Macs, and are now the recommended way of building your UI.

* View controllers — NSViewController objects — are now placed in the responder chain. (Previously we had to manually place them in the responder chain.)

* The NSViewController API is now very similar to the UIViewController API. It would be instantly familiar to any iOS developer.

* NSViewController has support for containment, with some built-in containers (split views, tab views) and the ability to write custom containers.

Macs already had Auto Layout support, and of course lots of frameworks such as Foundation and Core Data are Mac frameworks too. (Often they were originally Mac frameworks.)

The weirdest thing for iOS developers doing a Mac app was probably the old way of doing outlines and table views — there was that old NSCell API. But we’ve had view-based tables and outlines for a while now, so that’s not a consideration any more.

And the Mac has some nice things that don’t exist on iOS. For instance, wiring up a checkbox in a preferences screen to NSUserDefaults requires no code whatsoever, since you have Cocoa bindings on the Mac.

You might not want to write Mac apps. That’s fine. But AppKit has just taken some very nice ideas from UIKit, and that’s a cool thing, and worth noting.
