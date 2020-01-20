@title On Replacing OperationQueue
@pubDate 2020-01-20 12:37:14 -0800
@modDate 2020-01-20 12:37:14 -0800
We fixed our [mystery KVO crash](https://inessential.com/2019/12/30/kvo_my_enemy) by writing a replacement for `OperationQueue.`

Well, sort of a replacement. It’s not a drop-in replacement, because what we really wanted was slightly different from `OperationQueue`.

`OperationQueue` does a few things:

* Manages a queue of operations
* Runs operations in multiple threads
* Supports dependencies — operations can be dependent on other operations
* Supports canceling operations

But that’s not exactly what we want. We want something that:

* Manages a queue of operations
* Runs operations *on the main thread*
* Supports dependencies — operations can be dependent on other operations
* Supports canceling operations

Note the difference: we want to run operations on the main thread. That may sound crazy to you, but I’ll explain why shortly.

Note also some characteristics of `OperationQueue`:

* Uses KVO (is finicky and crashy)
* Subclassing is allowed and expected (of `Operation`/`NSOperation`)

But that’s not what we want either. Instead, we want:

* Low-tech, non-crashy notifications
* No subclassing

#### Canceling Is the Most Important OperationQueue Feature

Recall that `OperationQueue` — at the time just `NSOperationQueue` — came out before Grand Central Dispatch (GCD), and it was the best way to get code off the main thread.

But these days we do have GCD, and when we want to run code on a background thread, we use GCD. (And, often, a serial queue.) We don’t need `OperationQueue` just to be able run code on multiple threads.

Instead, the important thing about `OperationQueue`, the reason to use it instead of just using GCD, is the ability to cancel operations. This is critical in an app where conditions change — the network might fail, the app might move to the background, databases may get closed. Canceling is critical.

This is why we didn’t just stop using `OperationQueue` in favor of GCD. This is why we needed to write our own thing that supports canceling.

#### Why Run Code on the Main Thread

I’ve written before about [writing main-thread-only code](https://inessential.com/2015/05/22/how_not_to_crash_4_threading) — it’s a paradise when you don’t have to think about concurrency.

You may think you’re good at writing thread-safe code, but are you 100% good? Is everyone on your team as perfect as you are? And, when multithreading bugs inevitably do happen, how quickly can you reproduce them and fix them?

Our default position is to write code that is not thread-safe — and not even safe to run on any thread besides the main thread.

That said, we do have a number of APIs that do async things and then call back to the main thread. Networking, for instance. Updating or querying a database. Parsing feeds.

Even though our operations run only on the main thread, they can — like any other code — call an API that does something on a background thread and then calls back to the main thread.

An operation’s code might look conceptually like this:

	func run() {
		// On the main thread right here.
		// doSomeAsyncThing uses GCD
		doSomeAsyncThing(args) { result in
			// Back on the main thread.
			guard !isCanceled else {
				return
			}
			doSomething(result)
			informDelegateOfCompletion(self)
		}
	}

To sum up: because we have GCD, we don’t need an operation queue that handles concurrency. In fact, we don’t even *want* it to handle concurrency.

#### MainThreadOperationQueue, MainThreadOperation

[MainThreadOperationQueue](https://github.com/Ranchero-Software/RSCore/blob/master/RSCore/MainThreadOperationQueue.swift) and [MainThreadOperation](https://github.com/Ranchero-Software/RSCore/blob/master/RSCore/MainThreadOperation.swift) are part of our RSCore framework.

A few things to note:

* `MainThreadOperation` is a Swift protocol. You don’t subclass it; you implement it.
* When an operation is finished, it informs the queue by calling a method on the main thread. No KVO or other form of notifications.
* The code is quite simple, but there’s more of it than you might expect: managing dependencies adds to the bulk. The code is basically just a thing that does a bunch of housekeeping.
* It uses `precondition(Thread.isMainThread)` in a number of places, which will crash even a Release-build app. We use `precondition` over `assert` quite deliberately: if these functions are called outside the main thread, then we’re operating in a surrealistic environment, and we refuse to go on.
* [It has some tests](https://github.com/Ranchero-Software/RSCore/blob/master/RSCoreTests/MainThreadOperationTests.swift), but of course it should have more tests.

At this writing, this code is already running on over 2,300 iOS devices, since it was included in [NetNewsWire 5.0 TestFlight build 28](https://nnw.ranchero.com/2020/01/19/netnewswire-for-ios.html) last night. That was the build where we switched our Feedly syncing code from `OperationQueue` to our own `MainThreadOperationQueue`. (I just checked number of installations in App Store Connect.) So far so good!

One bonus thing I like about it is that any given `MainThreadOperation` can create its own `MainThreadOperationQueue` to run a bunch of child operations, and then call back only when those operations have finished or are canceled. (We use this feature as part of Feedly syncing.)

But my favorite thing about it is how low-tech it is. There’s not even a hint of cleverness in that code — it’ll put you to sleep. But this makes bugs, including crashing bugs, way less likely.

#### Don’t Do This (Usually)

Normally I am very much against reinventing wheels. No points are awarded for writing your own version of a thing that 1) comes with the system and 2) is well-suited to your needs — instead, points are taken *away* for showing off and wasting time.

Even if a system-provided thing is not exactly right, but close enough, you should probably use it.

But when you do find you need write your own version of the wheel, think about what you need exactly, and just do that thing and not more. And don’t be clever — you don’t want to trade one problem for another.
