@title Frontier Diary #1: VM Life
@pubDate 2017-04-03 13:44:34 -0700
@modDate 2017-04-03 13:44:34 -0700
It’s been years since I could build the <a href="http://frontierkernel.org">Frontier kernel</a> — but I finally got it building.

It’s really a ’90s Mac app that’s been Carbonized just enough to run on MacOS, but it’s by no means modern: it uses QuickDraw and early Carbon APIs. It’s written entirely in C.

I got it building by installing MacOS 10.6.8 Server in VMWare. Installed Xcode 3.2.6. And now, finally, I can build and run it.

#### What is Frontier?

Frontier — as some of you know — was a UserLand Software product in the ’90s and 2000s. I worked there for about six years.

The app is a development environment and runtime: a persistent, hierarchical database with a scripting language and a GUI for browsing and editing the database and for writing, debugging, and running scripts.

The <a href="http://scripting.com/frontier/snippets/nerdsguide.html">Nerd’s Guide to Frontier</a> gives some idea of what it’s like, though it was written before many of the later advances.

Maybe you’ve never heard of it. But here’s the thing: it was in Frontier that the following were either invented or popularized and fleshed-out: scripted and templated websites, weblogs, hosted weblogs, web services over http, RSS, RSS readers, and OPML. (And things I’m forgetting.)

Those innovations were due to the person — <a href="http://scripting.com/">Dave Winer</a> — and to the times, the relatively early web days. But they were also in part due to the tool: Frontier was a fantastic tool for implementing and iterating quickly.

#### The Goal

The high-level goal is to make that tool available again, because I think we need it.

The plan is to turn it into a modern Mac app, a 64-bit Cocoa app, and then add new features that make sense these days. (There are so many!) But that first step is a big one.

The first part of the first step is simple, and it’s where I am now: mass deletions of code. Every reference to THINK_C and MPWC has to go. All references to the 68K and PPC versions must go. There was a Windows port, and all that code is getting tossed. And then I’ll see the scale of what needs to be done.

(Note: my repo is a fork, and it’s not even on the web yet. The code I’m deleting is never really gone.)

I’m doing a blog diary on it because it helps keep me focused. Otherwise I’m jumping around on my side projects. But if I have to write about it, then I’ll stay on target.
