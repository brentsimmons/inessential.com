@title You’re Practically a Mac Developer
@pubDate 2018-04-25 13:27:25 -0700
@modDate 2018-04-25 15:09:38 -0700
Say you write an iOS app, and now you want to write the Mac version.

Assuming there’s a data model, maybe a database, some networking code, that kind of thing, then you can use that exact same code in your Mac app, quite likely without any changes whatsoever.

That leaves the 20% or whatever that’s user interface. AppKit is not the same as UIKit, but it’s recognizable. Same patterns and concepts, and often similar names (UITableView/NSTableView).

Given that you’ve done the hard thing — learning UIKit, Xcode, and Swift and/or Objective-C — taking the next step and learning AppKit seems like a very small thing. You’ve climbed the mountain already, after all.

You might complain that AppKit has some weird stuff. True. Some of it, though, isn’t truly weird — it’s just weird to you if you’ve never dealt with things like a menubar and multiple, live-resizable windows.

People coming *from* AppKit to UIKit (few people these days; many people 10 years ago) might also complain about safe content area insets (or whatever the thing is these days) and size classes and all manner of strange stuff they like not having to deal with in Mac apps. UIKit’s weird too, to some people.

Ten years ago I thought that all the new iOS developers would translate to lots more Mac developers. That that didn’t happen is a huge surprise to me. Because if you’re an iOS developer you’re practically a Mac developer *already*.

(And — little-known secret — the economics of Mac apps appear to be more favorable than for iOS apps.)
