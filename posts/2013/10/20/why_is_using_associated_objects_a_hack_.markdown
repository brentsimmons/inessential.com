@title Why Is Using Associated Objects a Hack?
@pubDate Sun Oct 20 14:14:48 -0700 2013
@modDate Sun Oct 20 14:14:48 -0700 2013
This came up on [Twitter](https://twitter.com/heathborders/status/391767563987734528) as a response to my post about <code>[NSURL&shy;Session&shy;Data&shy;Delegate](/2013/10/12/nsurlsessiondatadelegate_and_objc_runtim)</code>.

I’ll clarify.

I have a bunch of rules-of-thumb. One is that any time you <code>#import &lt;objc/runtime.h></code> in production code, you’re making a mistake. You’re hacking rather than doing the right thing.

The runtime is fun and interesting and every Cocoa developer ought to get to know it.

But if you find yourself resorting to runtime functions rather than using the non-runtime APIs as they are designed, you’re probably fighting the frameworks — and fighting the frameworks leads only to bad software and heartbreak.

Instead, it’s better to understand the non-runtime APIs and use them as they are designed to be used. (Think of the runtime APIs as [protomatter](http://en.memory-alpha.org/wiki/Project_Genesis).)

That said, of all the runtime APIs, associated objects comes the closest to getting a pass. The feature is convenient and useful, and with normal care is not going to have unintended consequences.

Nevertheless, I think of associated objects as a last resort, just because <code>#import &lt;objc/runtime.h></code> is a big red flag. If the non-runtime APIs — the APIs closer to the problem at hand — provide a way to do what you want to do, then that’s the way to go.

I’ve used associated objects before, and I may again. But, every time I do, I think of it as a failure and I try to understand what failed. It’s either a non-runtime API or my own design, or both, that failed. If it’s my design, I should fix it rather than take the shortcut.

So I can’t really say that using associated objects is a hack in the sense that you’re depending on undocumented behavior. It’s documented. It’s a hack in the sense that you’re taking a shortcut. There is a more appropriate way of solving the problem.

(Except when there isn’t.)
