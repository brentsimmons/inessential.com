@title URLSession’s Delegate Queue Should Be the Main Queue
@pubDate 2021-01-27 12:01:06 -0800
@modDate 2021-01-27 13:17:49 -0800
[Consider this line of code from RSWeb](https://github.com/Ranchero-Software/RSWeb/blob/2f7bc7671a751e994e2567c8221ba64e884d5583/Sources/RSWeb/DownloadSession.swift#L56), a framework NetNewsWire uses:

	urlSession = URLSession(configuration: sessionConfiguration, delegate: self, delegateQueue: OperationQueue.main)

The `delegateQueue` parameter specifies the queue for all delegate callbacks from URLSession — and here I’ve just gone and made it the main queue.

Some of you are screaming. I can hear you: “Brent, Brent, Brent — you’re going to block the main thread! Don’t do it!”

#### Let’s Back Up and Review the Documentation

The documentation says of the `delegateQueue` parameter that it’s…

>An operation queue for scheduling the delegate calls and completion handlers. The queue should be a serial queue, in order to ensure the correct ordering of callbacks.

(Pause right here and go check your own code to make sure you’re actually using serial queues. There’s a good chance you’re not.)

Given that the delegate callbacks should be on a serial queue, those callbacks should return as quickly as possible so that they don’t block subsequent calls.

You may have some expensive things to do — NetNewsWire, for instance, does RSS parsing and database updating. Those things should be <em>done on separate serial queues</em> — they should not be done on the delegate callback thread, because you don’t want to block it.

In other words, this all means that your delegate methods should be so fast that they wouldn’t block the main thread.

#### So Just Use the Main Thread

Your code that uses URLSession almost certainly has some data structures that do things like map a task identifier to some model object of some kind. You could go to lengths to make sure this is all thread-safe — and hope and pray nobody messes it up six months from now — or you could take the easy, safe route and go main-thread-only with that code.

That’s what we do with NetNewsWire. (And did with Vesper and other apps.)

It’s important to know I’m a performance junkie *and* a stability junkie — and with this practice I satisfy both.
