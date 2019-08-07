@title NetNewsWire Diary #3: The Crash Reporter
@pubDate 2018-12-18 13:32:12 -0800
@modDate 2018-12-19 13:08:55 -0800
The consensus choice for crash reporters is [PLCrashReporter](https://www.plcrashreporter.org/). It’s solid work.

So I went to add it to NetNewsWire, and here’s what happened:

Because of Apple’s new app notarization service, I needed to have PLCrashReporter get built along with the rest of the app — this way I could turn on the required “hardened runtime” setting. (Correct me if I’m wrong about this! <i>Update next day</i>: I *am* wrong. See postscript.)

But when I tried to build it there were a bunch of deprecation warnings (OSSpinLock, for instance) — and, since I treat all warnings as errors, it wouldn’t build. (I could turn that off, but I won’t.)

So I forked PLCrashReporter with the idea of fixing those errors myself, but then ran into territory I’m not familiar with and not confident about, so I stopped and deleted my fork.

#### So…

I thought some more about it, and did some research, and I learned that crash logs are still written to disk. This means I could use the crash log catcher I used to use in NetNewsWire 3 and NetNewsWire Lite 4.

The way it works: at launch time it looks for a crash log in the appropriate folder, and if the most recent crash log has not been seen before, then it prompts the user to send it it in. (A window appears with the text of the crash log, a place to add more info, and some buttons — send or don’t-send.)

This isn’t as slick as an in-process crash catcher — but this system worked for me for years. And it means one less dependency, and it means code I fully understand and control.

It’s a few dozen lines of code compared to adding an entire framework. So that’s what I’m doing.

#### The code

The code isn’t complete yet, but [here’s the start](https://github.com/brentsimmons/NetNewsWire/blob/master/NetNewsWire/CrashReporter/CrashReporter.swift). (And [here’s the code from NetNewsWire Lite 4](https://github.com/brentsimmons/NetNewsWireLite4/blob/master/RSCore/AppKit/RSCrashReportWindowController.m).)

I think this is the first time that I’ve looked back to old NetNewsWire code. I’m rewriting it in Swift, but using the same logic.

*Important note*: this code will *not* be part of the Mac App Store build. For that build, for better or worse, I’ll rely on Apple collecting and reporting crash logs. This crash reporter is just for the non-MAS build.

*PS* The crash catcher that appeared in earlier versions of NetNewsWire itself had a crashing bug (briefly): it would crash if there were no crash logs found! Which was self-healing — because once there was a crash log it wouldn’t crash any more. This remains my favorite bug ever. :)

*PPS* Shoutout to Uli Kusterer — my code was originally based on his [UKCrashReporter](http://www.zathras.de/angelweb/blog-ukcrashreporter-oh-one.htm).

*PPPS* The next day… I was wrong about needing to build PLCrashReporter in order to use the hardened runtime. On the Apple dev forums, [Quinn writes](https://forums.developer.apple.com/message/340768#340826):

>The hardened runtime is an attribute of the process.  It’s not something that frameworks can opt it to or out of individually.

So… I could just add a pre-built PLCrashReporter binary. But I’m going to stick with my thing anyway, again because it means one less dependency, and it means simpler, smaller code that I understand and control.

(The only remaining dependency like this is for [Sparkle](https://sparkle-project.org/). I don’t see any reasonable way of removing that.)
