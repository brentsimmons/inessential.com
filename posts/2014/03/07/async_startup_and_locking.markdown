@title Async Startup and Locking
@pubDate 2014-03-07 14:19:02 -0800
@modDate 2014-03-08 10:42:17 -0800
I try to avoid the following pattern, but it’s the best call from time to time.

Foo does some startup in a background serial queue. Parts of Foo’s public API don’t work until that startup has completed, so I want those methods to block callers until startup has completed.

I have not found a great way of dealing with this.

I do something like this:

    - init
      create_lock()
      lock()
      startupOnSerialQueue()
        completion: unlock()

    - someMethod
      lock()
      do_the_thing()
      unlock()

Ugh.

With this method, `someMethod` is blocked while <code>startupOn&#8203;SerialQueue()</code> is happening. This is good.

But `someMethod` also gets a lock all the rest of the time. That’s not a big deal, because, in practice, `someMethod` is super-fast. But it wouldn’t actually have to have that lock except right at startup.

This feels inelegant to me. It’s simple enough, and it works, but I don’t like it.

Do you know of a better solution?

My first thought is that `dispatch_once` would help — but it wouldn’t. (Not that I can see.) It would make sure `startupOnSerialQueue` is called once, but doesn’t solve the problem of blocking use of `someMethod` until `startupOnSerialQueue` has completed.

Another possibility: `someMethod` could put `do_the_thing()` inside a `dispatch_sync` block that runs on the background serial queue. But that also seems inelegant. Needlessly complicated.

This reminds me of the old joke. Man: “Doc, it hurts when I go like this!” Doctor: “Well don’t go like that!”

Except that I <em>will</em> go like that when everything else about the design is perfect. Since I can keep the async startup internal to Foo, it’s able to implement its public API without infecting anything else.

So my only question is if there’s a better pattern for handling this.

<i>Update 4:30 pm</i>: To be clear: I believe in serial queues. Absolutely love ’em.

I’ve had varied feedback on Twitter and email.

In the end, this is what I’m doing.

1. Using an NSLock property — self.startupLock — instead of a pthread\_mutex\_t. (I always forget about NSLock. But it’s easy and cleaner-looking than pthread mutexes.)

2. Not just unlocking the lock upon startup completion but nilling it out (as [Justin Miller](https://twitter.com/incanus77/status/442073285241475072) and others have suggested) since it’s no longer needed once unlocked. (In my specific case all access is main thread only, so this is fine.)

In the end this still isn’t beautiful, but it’s simpler and less code than everything else and it solves the problem of making sure that 1) startupOnSerialQueue() doesn’t block the main thread, and 2) someMethod blocks until startupOnSerialQueue() completes, and is fast the rest of the time.

The most interesting of the feedback suggested that this is a job for continuations and futures. So: something to learn. I’ll start with [Mike Ash’s article on futures](https://www.mikeash.com/pyblog/friday-qa-2010-02-26-futures.html).

<i>Update 10:30 am the next day</i>: Here’s what I really ended up doing.

Note that the previous solution had a deadlock. Sheesh. It was dumb anyway.

Instead I’m just doing startupOnSerialQueue via dispatch_sync. No lock needed.

So it blocks the main thread, but it’s not noticeable. (It’s about as fast as reading a 5K binary plist from disk, which I hadn’t realized at first. That’s not what it’s doing, but performance is comparable.)

Were startupOnSerialQueue slower, I’d have to think of something else. But since it’s fast enough, it’s fine.

So it looks like this:

<code>- init</code><br />
<code>&nbsp;&nbsp;dispatch\_sync (startupOnSerialQueue())</code><br />
<br />
<code>- someMethod</code><br />
<code>&nbsp;&nbsp;do\_the\_thing()</code>
