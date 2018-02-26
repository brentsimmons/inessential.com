@title Swift 1.2 Beta
@pubDate 2015-02-09 12:28:20 -0800
@modDate 2015-02-09 12:28:20 -0800
I didn’t expect to see this much improvement before WWDC. I’m *very* pleased.

Having accepted that Swift is <a href="http://en.wikipedia.org/wiki/The_Odd_Couple_(TV_series)">Felix Unger</a> to Objective-C’s Oscar Madison, I welcome changes that make Swift’s persnicketiness easier to satisfy.

My favorite change may be the improvements to <code>if let</code>. In the past, you’d write something like this:

<code>if let a = foo() {</code><br />
<code>&nbsp;&nbsp;if let b = bar() {</code><br />
<code>&nbsp;&nbsp;&nbsp;&nbsp;doSomething(a, b)</code><br />
<code>&nbsp;&nbsp;}</code><br />
<code>}</code>

Now you can write:

<code>if let a = foo(), b = bar() {</code><br />
<code>&nbsp;&nbsp;doSomething(a, b)</code><br />
<code>}</code>

(And more: you can include conditions with a where clause.)

So simple, so welcome.

I’m not sure what I think about the new annotations for Objective-C: nonnull, nullable, null\_unspecified, and null\_resettable.

On one hand it’s a leakage from Swift into Objective-C — as if Felix is wearing down Oscar until he gives in and picks his clothes off the floor and washes his hands 50 times a day. And it’s not like this has ever been a problem for me in Objective-C. (Objective-C’s nil-handling behavior was a delight when I switched from C, and I still like it.)

On the other hand, maybe I’m worn down a little bit too, and I don’t mind if the tools help ensure that my code matches my intentions. Most likely, though, I’ll use these only with Objective-C code that Swift needs to know about, because it *will* make things easier when writing Swift.

There are a bunch of other solid changes: <a href="http://adcdownload.apple.com//Developer_Tools/Xcode_6.3_beta/Xcode_6.3_beta_Release_Notes.pdf">read the release notes</a> if you haven’t already. The day when I’m writing most code in Swift has just gotten closer.

With all the great things, we’re still not at Swift nirvana. I checked one of my favorite examples: impathic’s <a href="http://blog.impathic.com/post/99647568844/debugging-slow-swift-compile-times">one-liner that takes 40 seconds to compile</a>. It still takes about 40 seconds. But, well, that’s software development for ya.

PS Swift has a Set type now! I love sets. Use ’em all the time.
