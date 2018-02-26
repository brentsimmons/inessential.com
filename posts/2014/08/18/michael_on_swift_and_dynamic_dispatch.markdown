@title Michael on Swift and Dynamic Dispatch
@pubDate 2014-08-18 11:37:26 -0700
@modDate 2014-08-18 11:37:26 -0700
Michael Tsai, <a href="http://mjtsai.com/blog/2014/08/18/its-a-coup/">“It’s a Coup”</a>:

>The costs for not using message passing, on the other hand, can be high because they make the code more rigid. You cannot retroactively make compiled code more dynamic. And yet, since dynamic is not the default, the odds are that a lot more methods will be static than need to be. Most of the time, <code>objc_msgSend</code> is not why your code is slow, yet Swift acts like it needs to protect you from this.

I’m no fan of swizzling and don’t care what happens to it. I throw swizzling in the same bucket as SIMBL and APE and haxies, and I’m glad they’re not screwing up my apps these days. (Newer Cocoa developers have no idea what I’m talking about, I realize.)

But I *do* care about KVO. Very much. (Warts and all.)

This die-hard speed freak has never been concerned with the speed of <code>objc_msgSend</code>. I’ve noticed it in Shark and in Instruments, but the real performance issues were elsewhere in my code.

That said, it hasn’t escaped my notice that most of the time static dispatch would be fine. And most of my classes could be marked as final. So I’m not actually outraged or anything — I keep an open mind that I *would* actually get noticeably better performance from Swift.

Especially given that now we do have the <code>dynamic</code> modifier.

Objective-C is supple by default. Amazingly so. But I shouldn’t pretend I use that suppleness more than I do. And if Swift isn’t so supple — well, that’s probably closer to what we actually need than what we think we need.

Still, though, there is code in Vesper that can’t be ported to pure Swift. (Model code.) The point that you can <em>use</em> something like Core Data but couldn’t <em>write</em> it in Swift remains important. But, then, Swift is young, not even 1.0, and part of the deal is that it’s up to us developers to communicate our needs.
