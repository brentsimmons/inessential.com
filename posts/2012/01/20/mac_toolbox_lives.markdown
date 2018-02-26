@title Mac Toolbox Lives
@pubDate Fri Jan 20 15:43:03 -0800 2012
@modDate Fri Jan 20 15:44:24 -0800 2012
I enjoyed Gwynne Raskind’s two posts about the Mac Toolbox on Mike Ash’s blog.

<a href="http://mikeash.com/pyblog/friday-qa-2012-01-13-the-mac-toolbox.html">Friday Q&A 2012-01-13: The Mac Toolbox</a>

<a href="http://mikeash.com/pyblog/the-mac-toolbox-followup.html">The Mac Toolbox: Followup</a>

During my rare spare cycles, I’ve been working on updating a Toolbox app which was Carbonized just enough to run on OS X back in 2001.

It still runs now, yes, but years have passed, and many of the APIs it uses have been deprecated. I can’t even use Xcode 4 to build it — I have to boot back into Snow Leopard and use Xcode 3.

The biggest challenge with this app, by far, is dealing with QuickDraw. I’ve already switched from Open Transport to sockets and switched from old date APIs to NSDate and related APIs. But QuickDraw is the black beast, since it’s so unlike Quartz.

Among other things, it’s given me the opportunity to learn Core Text, which I hadn’t had a need for until now — but which I will need soon in my job.

The code is a great reminder of how far we’ve come and how much easier many things are now. For example: this code has switch statements for which part of a scrollbar was hit. It calls WaitNextEvent. It uses cooperative threading (which meant using non-blocking sockets). It’s got lots of globals. It’s written in C (but using a very object-oriented style, with structs, function pointers, and callbacks).

Eventually I’d like to make it a Cocoa app — but the first step is replacing deprecated APIs and being able to build on Lion using Xcode 4.x. (It still <em>runs</em> on Lion, at least.)
