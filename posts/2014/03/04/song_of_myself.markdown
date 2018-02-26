@title Song of Myself
@pubDate 2014-03-04 12:00:50 -0800
@modDate 2014-03-04 12:51:33 -0800
Rich Wardwell [talks about the weakSelf dance](http://blackpixel.com/blog/2014/03/capturing-myself.html):

>The best way to handle retain cycles in blocks is to prevent the cycle from occurring in the first place. Using the `weakSelf` dance is easy.

Like Rich and probably everybody else, I love blocks. I couldn’t go back.

The weakSelf thing is the least lovely part of blocks, though. The second least-lovely is the syntax: I rely on auto-complete and [fuckingblocksyntax.com](http://fuckingblocksyntax.com/), which I’ve bookmarked. (Neither of these puncture my big red balloon of affection for blocks.)

Some things I’ve noticed about my own use of blocks:

* Almost all of my blocks are stack-based. I rarely copy a block and assign it to a property. (Not never, though.)

* I can often avoid the weakSelf dance by thinking about what’s really needed. My first thought is always that self is somehow needed — but that often turns out not to be true. (Not always.)

* I never use <code>-[NSNotificationCenter addObserverForName:&#8203;queue:&#8203;usingBlock:]</code>.

<i>Update 12:25 pm</i>: [Kyle Sluder says](https://twitter.com/optshiftk/status/440942587600707585):

>I’d say the least lovely part about blocks is the automatic temporary shadow variables clobbering data: [http://llvm.org/bugs/show…](http://llvm.org/bugs/show_bug.cgi?id=15649)
