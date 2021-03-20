@title How NetNewsWire Handles Threading
@pubDate 2021-03-20 14:08:25 -0700
@modDate 2021-03-20 14:08:25 -0700
NetNewsWire is mostly *not* multi-threaded. Here’s what we do:

#### Run Most Code on the Main Thread

The default place for *all* of our code — UI code and otherwise — is the main thread. Synchronous code running on the main thread is the easiest code to reason about and is the least likely to trigger weird, intermittent bugs.

In other words: we try, as much as possible, to not use queues or threading at all. I can’t emphasize this enough: the *best way to handle concurrency is just to not do it*.

#### Communicate Between Components on the Main Thread

Every notification and every callback happens on the main thread.

Though a given object (or small system) may use a serial queue internally, it never, ever lets that fact leak out beyond its own boundaries.

#### Use Serial Queues for Pure Functions That Take Time

Parsing an RSS feed is a pure function. Since it does take some time (though less than you think), it can be done on a serial queue, in the background. The result is returned via callback on the main thread (see above).

These kinds of things are great for background processing because they’re perfectly isolatable — parsing a feed affects no state. It doesn’t do any notifications. All it does is callback, once done, with an object.

There are other examples (decoding JSON or image data) that are great for this, and which we handle the same way.

#### Use Serial Queues for Database Access

Our model objects are plain ol’ classes and structs. The APIs for reading and writing are main-thread-only, and they call back asynchronously but always on the main thread with a result.

Inside the database code, though, is a serial queue. It’s completely internal to that code, though, and utterly invisible to the rest of the app.

When the database code sends any notifications, it does so on the main thread. It doesn’t otherwise affect any app state.

#### Use Asserts and Preconditions

If you do a search on `Thread.isMainThread`, you’ll find a bunch of these…

	precondition(Thread.isMainThread)

…and…

	assert(Thread.isMainThread)

…and one example of `XCTAssertTrue(Thread.isMainThread)`. We don’t otherwise test if we’re in the main thread.

(I would not mind having a whole lot more of `precondition(Thread.isMainThread)` than we do now.)

### The Result

You may be skeptical about this model, but I’ll remind you that NetNewsWire is responsive and freakishly fast. It’s also — by *far* — the most stable and bug-free app I’ve ever worked on in my long career. And a big part of that is our threading model.

One of the nice things about this model is that a developer knows, just by looking at where they are, what thread the code is running on. It’s almost always main. But if you’re working on the RSS parser or similar, you know that it literally doesn’t matter, and if you’re working on the database or similar, it’s obvious that you’re using a serial queue.

As we adopt Combine, SwiftUI, and future Swift language changes to support concurrency, we will continue to use this model. The details of our implementation may change, but the model will remain the same: use the main thread everywhere except in a few cases, and make sure that those cases cannot leak knowledge or behavior of their queues outside themselves.

### Advice

Some developers I’ve known seem to think that being good at concurrency makes them badass. Others seem to think that senior developers must be great at concurrency, and so they should be too.

But what senior developers are good it is eliminating concurrency as much as possible by developing a simple, easy, consistent model to follow for the app and its components.

And this is because concurrency is too difficult for humans to understand and maintain. Maybe you can create a system that makes extensive use of it, and have it be correct for one day. But think of your team! Even if you’re a solo developer, you and you-plus-six-months makes you a team.

I know you’re worried about blocking the main thread. But consider this: it’s way easier to fix a main-thread-blocker than it is to fix a weird, intermittent bug or crash due to threading.

With a main-thread-blocker, use the Time Profiler in Instruments and figure out what’s going on. It may be that something does need to move to a background serial queue — or, more likely, there’s a data structure or algorithm that could be improved, or you find your app is doing unnecessary work (or both).

#### How To Get There From Where You Are

I suspect most apps don’t have a clear model for concurrency. If yours does, then great! Skip the rest of this post. :)

If you want to move to the model I’ve described above, I’d start with a few things.

* Identify code that should be main-thread-only and use `assert(Thread.isMainThread)` in that code
* Turn on Xcode’s Main Thread Checker
* Make sure that every Notification that your app posts is posted on the main thread. In notification handlers, add an `assert(Thread.isMainThread)`

If you don’t use Notifications, apply that advice to KVO or whatever else you might be using.

The reason I pick Notifications and KVO is because they’re a kind of spooky action at a distance — when you’re working on the Notification handling side, you don’t know what thread the Notification was posted on, and developers tend to assume it’s the main thread. This is a common place for threadedness to leak, which causes bugs and crashes. (Accidental multithreading is the scourge of our platform.)

The next step is probably to look at the places where you’re using queues and find out which of those could be moved to the main thread. And, when you can’t move to main, build better walls: make APIs that call back on the main thread, and don’t let the fact of those queues leak out from behind the API. Don’t let threadedness leak.

You can get there incrementally.

In the meantime you may find that you’re having to dispatch to the main queue rather often as a defensive measure.

Ideally, you’re only dispatching to the main queue when it’s part of this threading model (when posting a notification from a background queue or calling a callback) and never as a defensive measure.

However, it may be a while before your app gets there, and that’s okay. (Tip: do consider the case where sometimes that call to `DispatchQueue.main.async` is happening in code already running on the main thread. The async part is real, and you may not always want that: sometimes you may want code to run immediately when already on the main thread. And sometimes not.)

In the end: change all your `assert(Thread.isMainThread)` to `precondition(Thread.isMainThread)` — make your app crash in production when the threading model is violated. Being able to do that — knowing that it won’t ever trip — is a great place to be. 🐣🐥🎉
