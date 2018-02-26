@title Some notes on threading
@categoryArray Cocoa-Development
@pubDate Sun Dec 05 16:06:38 -0800 2010
@modDate Fri Feb 18 11:54:44 -0800 2011
My current, barely-organized thoughts on threading and Cocoa apps:

### Main Thread Gravity

Communication between systems always happens on the main thread. (A system is one or more objects that work together.) In most cases, communication between objects in the same system happens on the main thread too.

If an object does something in the background, that is that object’s business and nobody else’s.

This extends to notifications: from background threads, I always make sure notifications get posted on the main thread. This way every notification observer can always assume that it’s getting called on the main thread.

I think of threads as like hang-gliding — dangerous and fun, aloft for a little while, but you always come to earth. The key is to *land*, not crash.

I’m very deliberate about my threading. I like Grand Central Dispatch, but for my purposes NSOperationQueue works best. (I’m doing web services stuff mostly: downloading, parsing files, storing stuff in databases. The formal, easily-monitored approach of NSOperationQueue works best here.) I definitely recommend against anything but GCD and NSOperationQueue — anything else (NSThread’s detach method, etc.) is too random. (Yes, we used it for years, but we have better stuff now.) (In fact, I almost never even use NSInvocationOperation — I much prefer the structure and defined stop/start of NSOperation.)

I use an NSOperation subclass that takes a target and selector in its init method. When it’s finished, it calls the target and selector on the main thread. This way the caller only ever sees the main thread — it creates the operation on the main thread, then gets called back on the main thread. The fact that the operation happens in the background is unknown to the caller: the caller just knows that it’s async, and doesn’t know anything else.

KVO is a trickier thing. Here’s how I handle that: anything happening in a background thread is not observable (by convention). Whatever is going on is private. When it’s time to set public stuff, stuff that could be observed, those things are set on the main thread.

Here’s an example: I do XML parsing in an operation on a background thread. You could imagine another object wanting to observe changes — for instance, whatever object is charged with saving data to a database might want to observe the XML parser.

But I just don’t do it that way. Instead, the XML parser defines a protocol and can take a delegate. It calls the delegate when certain defined things happen. In this case, yes, the communication all does happen on the background thread, but only because the XML parser and the data-saver delegate are intimates, working together in the same system. But the link between them is still thin and well-defined (just two methods in a protocol).

Make sense? I’ll sum up:

1. Stuff happening in threads is private and self-contained. Black boxes, train cars.

2. Communication between two things should be on the main thread, except in carefully controlled circumstances. Communication includes notifications and KVO, not just direct calls.

3. Using GCD or NSOperationQueue is way better than the old ways of doing threading.

### Reviewability

This is probably my favorite reason for using NSOperation for all threading: I can see *everything* that happens in background threads just by looking at my NSOperation subclasses.

This is so much easier than the old way, where I might look at any method in any class and not know, at a glance, whether or not it was running in the main thread or other threads.

Sure, I could have organized things better. I would have invented something like NSOperation. Since it exists now, I just use it.

When it comes to threading, you want to look, and *know* — you never want to guess.

### Locking

Locking sucks. If you have to do it, you have to do it. It doesn’t mean you’ve failed — failure would be not-locking when you really do need a lock.

Here’s a thing to think about: can you define an expensive, self-contained operation that doesn’t need locking? If so, then that’s a great candidate for something that could go on a background thread. XML parsing, again, is a great example.

There are a couple other things you can do which make sense.

1. Use performSelectorOnMainThread to set some data that would otherwise require locking. (This is not a trick to use willy-nilly, though — typically it comes at the very end of an operation, not sprinkled throughout.)

2. Use NSCache — it’s thread-safe.

As a developer, I always find it interesting to read about lock-less techniques and memory barriers and various cool stuff. But I never, ever code with that stuff. (I assume these things are used behind the scenes, in the frameworks and runtime, which is totally cool. I’m happy to let the super-smart engineers at Apple make stuff faster.)

Here’s the thing about code: the better it is, the more it looks and reads like a children’s book. Bad code looks like James Joyce wrote it. (When it comes to app development, that is. Compilers, runtimes, kernel extensions — maybe they’re different beasts. I don’t know.)
