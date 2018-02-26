@title The Long and Short Paths for Frontier on Mavericks
@pubDate 2013-11-17 13:06:02 -0800
@modDate 2013-11-17 17:38:04 -0800
Dave Winer wrote about <a href="http://scripting.com/2013/11/17/optionsForFrontiermacUsers">choices for Frontier/Mac users</a>, now that Frontier and the OPML Editor won’t run on Mavericks.

The earliest comment I can find is from August 20, 1990, though it appears the project was started before then. It’s old code, and it doesn’t look anything like what a modern Mac programmer would write. (It’s written in C, at least, and not C++. Thank goodness. You’ll notice lots of structs and function pointers.)

There are all kinds things that would have to be fixed before it could be made a modern Mac app. Here are some of them:

* Relies too much on globals.

* Uses QuickDraw. Switching to Quartz is *not* a straightforward change.

* Uses Open Transport instead of sockets.

* Memory is mostly Handles and Pascal strings. (There’s no Cocoa Foundation in there, and only the most minimal use of CoreFoundation.)

* Switching to 64-bit may be a major challenge because of the database format.

* It uses cooperative multitasking rather than preemptive. (YieldToAnyThread()!)

* Though it was Carbon-ized, it still uses WaitNextEvent rather than Carbon events and timers.

* It uses a bunch of other deprecated APIs: file system, resource manager, etc.

* You can’t compile it on Xcode 5. Which means you really need a machine running OS X 10.6 and Xcode 3.x with the 10.5 SDK. That’s the only way you can build and debug, so you can understand how it’s supposed to work.

* Text editing uses a third-party library called Paige which should be just nuked in favor of the built-in text editor.

* String objects are not Unicode-aware. (There are some translation verbs, but basically the system expects strings to be MacRoman-encoded strings with single-byte characters.)

* There are some things that should probably be nuked: running as an OSA component, displaying IOA (MacBird) cards, menu-sharing.

* This same codebase builds a Win32 app. Most of the code is shared. This just adds to the complexity of making any changes.

* Plus things I’m not thinking of.

#### The Slow Path

Dave mentions that it’s organized in layers, and it is.

I recommend starting with the database layer. Make it so that it doesn’t use globals and does us preemptive instead of cooperative threads. Make sure it’s thread-safe. Make it compile for 64-bit, and make it so a database file created on a 64-bit Mac can be opened in 32-bit mode. (Though you might allow the exception that databases beyond a certain size can’t be opened in 32-bit mode.)

Ideally this would be a project itself, one that could also build as a stand-alone library (which was [done once in the past](http://scripting.com/davenet/1996/09/05/ODBEngine10.html)). (For those who don’t know: the database is a key-value tree structure. Tables can hold tables, scalars, scripts, and some pre-defined objects. The language uses dot notation to refer to things.)

The next thing to tackle would be the language, the compiler and evaluater. Same issues apply: it shouldn’t use globals, it should be thread-safe, and it should be 64-bit. Ideally it could compile with its only dependency the database layer.

I would say repeat until finished, and that’s partly true, but eventually you get to the UI. I would structure things this way: the UI would be Cocoa and not shared with the Windows version. The database, language, utilities, and other low-level things would remain written in C and shared with Windows.

I described this path in just a few paragraphs, but it’s bigger than it sounds.

#### The Short Path

There is, however, a shorter path to getting it up-and-running on Mavericks. The main issue is that Open Transport went away, and the networking layer should be replaced with sockets.

I’ve actually done this work already. It needs more testing and surely needs some fixes, but it exists and does at least work to the extent that I tested it.

The problem is that I don’t have a machine capable of running OS X 10.6. If I did, I could get Xcode 3.x and the OS X 10.5 SDK and do a build that would run on Mavericks.

But if you’re a programmer and have such a machine, please feel free. Here’s [MacSocketNetEvents.c](http://ranchero.com/downloads/MacSocketNetEvents.c), which replaces OpenTransportNetEvents.c.

So: that would get it back up on Mavericks. It would still be a 32-bit app and the to-do list would still be huge — but at least it would *work* again. (Until the next OS X release, anyway.)

*Update 5:35 PM Pacific*: you’ll also need [mutex.h](http://ranchero.com/downloads/mutex.h) and [mutex.c](http://ranchero.com/downloads/mutex.c).
