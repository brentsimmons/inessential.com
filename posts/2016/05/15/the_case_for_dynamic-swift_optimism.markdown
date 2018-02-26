@title The Case for Dynamic-Swift Optimism
@pubDate 2016-05-15 17:22:46 -0700
@modDate 2016-05-15 17:22:46 -0700
In my <a href="http://inessential.com/2016/05/14/the_tension_of_swift">last</a> <a href="http://inessential.com/2016/05/15/a_hypothetical_responder_chain_written_i">two</a> posts I brought up my nervousness over not seeing dynamic features in Swift yet — because I argue that Objective-C’s runtime is a big part of what makes AppKit and UIKit awesome, and any future frameworks need to be just as awesome.

I should perhaps not be so nervous.

I strongly suspect that Swift is designed with dynamic programming in mind — and is potentially better for dynamic programming than Objective-C. (Since, after all, it drops the C, is a fresh start that learns from the past, doesn’t have to worry about breakage so much — and, hey, look at that team.)

If this is true — and I don’t have an easy way to evaluate it, so I’ll assume it — then we can assume that the reason it hasn’t been an issue so far is that we already have the Objective-C runtime. (Even if all your code is Swift, your app is using that runtime.)

So there’s no rush.

However, open-source-Swift means there are environments where the Objective-C runtime is not present. Which means the calls for dynamic programming may come from, ironically, web developers running Swift on Linux.

But there’s an even bigger point: lots of people in Apple write apps. They’re the first consumers of Swift and hypothetical Objective-C-runtime-free frameworks. They’re going to need to be able to write their apps too.

So I shouldn’t be so nervous.
