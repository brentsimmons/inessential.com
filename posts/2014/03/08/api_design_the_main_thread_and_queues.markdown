@title API Design, the Main Thread, and Queues
@pubDate 2014-03-08 11:34:50 -0800
@modDate 2014-03-08 11:44:44 -0800
Jonathan Grynspan [writes on Twitter](https://twitter.com/grynspan/status/442317023226236928):

>In the general case, requiring single-threadedness is a code smell or worse.

He was reacting to my [previous post](http://inessential.com/2014/03/07/async_startup_and_locking) mentioning the requirement that an API is main-thread-only.

I disagree with Jonathan. I’ll describe why and what I do.

#### The ideal Cocoa app

In the best-case scenario, that exists only in our dreams, everything runs on the main thread. We don’t need queues or threads because everything is so fast.

In this ideal world we never have to think about concurrency because there’s no such thing.

I’ve never written an app this way and I’m sure I never will. (As computers and devices get faster, apps will be expected to do more.)

But it’s still worth keeping this ideal in mind.

#### The UI runs on the main thread

There’s no escaping this. The main thread has gravity — code paths tend to start there and end up there.

There’s nothing wrong with recognizing the special-ness of the main thread.

#### Thread-safety is difficult

You can use a mix of queues, immutable data, and locking, and still get it wrong. Thread-safety is notoriously difficult.

The way to deal with concurrency is *not* to make everything thread-safe. (That may not be true for server apps, but it’s true for client apps.)

Making everything thread-safe is a lot of effort, and it’s easy to make mistakes. Due to the nature of concurrency bugs, some of those mistakes will show up only as intermittent bugs that are hard to diagnose. The developer may not be able to reproduce them.

#### What I do

I start with the ideal assumption that everything will run on the main thread.

Once I find that a queue is needed, I keep that queue private to the object that uses it. That object’s public API is main-thread-only, even though internally it uses a queue.

That object’s API may take completion callbacks, and those tend to be called on the main thread.

(I make an exception for objects that work very closely together. That’s fairly rare.)

A typical example:

<code>- (void)notesWithUniqueIDs:&#8203;(NSArray \*)uniqueIDs fetchResultsBlock:&#8203;(QSFetchResultsBlock)&#8203;fetchResultsBlock;</code>

The method triggers a fetch from the database on a background serial queue. Once complete, it calls `fetchResultsBlock(notes)` on the main thread.

Behind the scenes that object has to deal with concurrency: it fetches notes and updates a cache of uniqued notes. But those concurrency issues are small, well-defined, and limited to the scope of that object — and the caller never, ever has to think about it.

This system works wonderfully well. It doesn’t block the main thread because it *does* use background queues. And it makes dealing with concurrency as mistake-free as possible because most of the code can assume, correctly, that it’s running on the main thread.
