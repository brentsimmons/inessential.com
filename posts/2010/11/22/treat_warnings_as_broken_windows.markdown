@title Treat Warnings as Broken Windows
@categoryArray Cocoa-Development
@pubDate Mon Nov 22 10:13:02 -0800 2010
@modDate Fri Feb 18 11:55:19 -0800 2011
The more years of programming experience I get, the more I like having my tools tell me about problems and potential problems.

Lately I’ve been switching my projects to use the same <a href="http://boredzo.org/blog/archives/2009-11-07/warnings">set of errors and warnings Peter Hosey uses</a>.

I even turn on treat-warnings-as-errors — what Peter calls “hardass mode” — because, well, I want to be forced to stop and fix whatever it is.

(“Hardass mode” also simplifies my thinking: instead of two types of problems, there’s just one, and it has to be fixed right away. Any time you can simplify and thereby benefit, it’s good. We deal with plenty enough complexity already.)

Peter also mentions running the Static Analyzer, but I’ll reiterate that point. Do it. There’s a setting that will make it run every time you do a build (so you don’t have to explicitly choose Build and Analyze).

With one of my projects (so far, more to come) I’ve also been running unit tests with each build. The unit tests are in a separate project, which I made a dependent project in the app, so that the tests run every time. It’s another simplification: I don’t have to think about remembering to run my tests — they just run every time. Cool.

<h4>Bigger picture: Broken Windows</h4>

Six years ago, Daring Fireball published <a href="http://daringfireball.net/2004/06/broken_windows">Broken Windows</a>, a great post talking about operating systems and malware:

<blockquote>It’s similar to the “broken windows” theory of urban decay, which holds that if a single window is left unrepaired in a building, in fairly short order, the remaining windows in the building will be broken.</blockquote>

I think there’s something similar with writing software. Consider the following bit of code:

<pre>NSInteger arrayCount = [someArray count];</pre>

In the real world that’s pretty unlikely to cause a bug. But it’s wrong, because count returns NSUInteger rather than NSInteger. Big deal, right? Most bugs occur at a higher level than this. They’re logic bugs that error-checking can’t catch.

So is there a real point to fixing these things?

YES. Because it <em>is</em> wrong, and because there <em>might</em> be bugs lurking in there. And having any doubt at all is like having a broken window.

Being a hardass about the correctness of my code has had a great effect on my mental state when programming. <em>Knowing</em> that all windows are intact (and clean and shiny and transparent) makes me respect it more — and respect the software and my own abilities — and that’s very much to the benefit of the software, even if sometimes I find myself fixing picayune stuff that I know (that I <em>think</em> I know) would never cause a problem anyway.

I used to think sometimes: “Hey, I’m a professional of many years. I know what I’m doing. I can break this rule because I know for sure it will be fine.”

I don’t allow that thought anymore. Instead, now I think: “Hey, I’m a professional of many years. I know what I’m doing. I’m wise enough to use every tool at my disposal to make sure my code is correct.”
