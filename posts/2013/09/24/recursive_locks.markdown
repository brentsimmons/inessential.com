@title Recursive Locks
@pubDate Tue Sep 24 11:33:40 -0700 2013
@modDate Tue Sep 24 11:38:00 -0700 2013
David Butenhof explains, in 2005 in comp.programming.threads, <a href="http://www.zaval.org/resources/library/butenhof1.html">why POSIX has recursive mutexes</a>: “Because of a dare.”

He also writes:

>First, implementation of efficient and reliable threaded code revolves around one simple and basic principle: follow your design. That implies, of course, that you have a design, and that you understand it. 

>A correct and well understood design does not require recursive mutexes.

Fiery Robot writes, in 2008, <a href="http://www.fieryrobot.com/blog/2008/10/14/recursive-locks-will-kill-you/">Recursive Locks Will Kill You!</a>:

>Better to use a real honest-to-goodness lock. This means that if a thread tries to lock a lock that’s already, well, locked, you’ll deadlock. This is good. I like this, just as I like crashes. I know, you think I’m crazy, but if you deadlock on your own thread, then you know you just did something bad.

Google Mac Blog writes, in 2006, in <a href="http://googlemac.blogspot.com/2006/10/synchronized-swimming.html">@synchronized swimming</a>:

>Shark told us without a doubt that we were paying heavily for the @synchronized block each of the millions of times we were calling fooFerBar… So, I wondered, how exactly does @synchronized work? And is there a cheaper way of getting the same thread-safe result?

(For new Cocoa developers: Shark was the performance profiler we used before performance profiling was added to Instruments.)

#### Which Locking System I Use

I haven’t used @synchronized in years. Not only is it recursive (which I tend to avoid), it sets up an exception handler. I would way rather have my exceptions go unhandled. (I don’t know if it’s still slow compared to other locking systems, but I strongly suspect it is.)

So there are two that I use:

* OSSpinLock. It’s great when contention is expected to be low. (Which is surprisingly often.) It’s super easy to use.

* Pthread mutexes. You can create these as recursive locks, though I try to avoid it.

(There’s one recursive lock in <a href="http://vesperapp.co">Vesper</a>, and I’m switching it to non-recursive — to OSSpinLock — today.)

Better, though, is to design so as not to need locks. Good use of GCD serial queues, blocks, and the main thread can often make locks unnecessary.
