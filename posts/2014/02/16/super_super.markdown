@title Super Super
@link http://optshiftk.com/2014/02/the-behavior-of-super/
@pubDate 2014-02-16 20:21:51 -0800
@modDate 2014-02-16 20:21:51 -0800
Omnizen and fellow Ballard-ite Kyle Sluder has some <a href="http://optshiftk.com/2014/02/the-behavior-of-super/">thoughts about the behavior of super</a>:

>It’s sometimes useful to skip the superclass’s implementation from within an override, calling the grandparent class’s implementation directly. (Bug workarounds are the primary use case that comes to mind.) This can’t be done with the <code>super</code> keyword, but the underlying <code>objc_msgSendSuper</code> runtime call can express this without any difficulty.

>I propose that the super keyword be extended to take an optional class argument.
