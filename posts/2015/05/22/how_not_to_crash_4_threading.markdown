@title How Not to Crash #4: Threading
@pubDate 2015-05-22 14:46:06 -0700
@modDate 2015-05-22 14:46:06 -0700
Here’s a simple rule: do *everything* on the main thread. Machines and devices are so fast these days that you can do more on the main thread than you think you can.

It’s a kind of paradise when you don’t have to think about concurrency *because there isn’t any*.

But…

I’m a performance junkie. Or, more to the point, I’m a user experience junkie, and the only thing worse than something being slow is being slow and noticeably blocking the main thread. Don’t do that.

I’ll get to that. But let’s start with the main thread.

#### The Main Thread Rule

All the code I write expects to run on the main thread and on the main thread only, with exceptions. (We’ll get to the exceptions in a minute.)

This solves a bunch of problems. For instance, I wrote in an earlier post about [unregistering for notifications in dealloc](http://inessential.com/2015/05/21/how_not_to_crash_3_nsnotification). A few people pointed out that you can’t guarantee on which thread dealloc will be called — but you *can*, actually, for any given object that runs on the main thread and is referenced only on the main thread.

It also means that any KVO changes are posted on the main thread, and any observing objects are also running on the main thread and expecting notifications on the main thread.

The benefits of not having to deal with concurrency are *tremendous*. I strongly suggest writing your entire app this way, and then testing to see if there’s anything that blocks the main thread. If not, then it’s golden, and you should ship. (Test with suitably large data, of course.)

#### Objects That Live in Their Own Little World

If — and only if — you find that the main thread is noticeably blocked should you look for ways to un-block it.

The first candidates are transformations that can be completely isolated from the rest of your app. I’ll use the example of processing JSON.

When I get JSON from a server, I like to turn it into intermediate objects that later get merged into model objects. Reasons:

1. I don’t want the model objects to know about JSON.
2. I want to deal with NSNull values, date conversions, and all other transformations before any other object sees the data.

So I use an NSOperationQueue or GCD queue (usually the latter, these days) to turn NSData returned by a server into intermediate objects.

(Always use a queue. Don’t ever use `detachThreadSelector` or `performSelectorInBackground`.)

These intermediate objects will be accessed by one thread at a time. They’re created on a background thread and then passed to the main thread, where they’re used to update the model and then discarded.

Because they *are* referenced on different threads during their lifetimes, I make sure that these objects never know about anything except themselves and what’s passed into their init methods. Once created on the queue, they’re immutable. They don’t observe anything and nobody should observe them (they don’t change, after all).

(This makes those objects fully thread-safe in the sense that objects that can’t change are thread-safe. However, it’s not necessary to stress the thread safety, because what’s important is that they’re safe to use on a single thread at a time, rather than on multiple threads at a time.)

#### Objects With Friends

Sometimes a number of objects work together. Instead of JSON, think of an RSS parser. In this example, there are three main objects involved: a SAX parser wrapper, its delegate, and the intermediate objects the delegate creates. (Conceptually exactly like the objects from the example above.)

The SAX parser wrapper and its delegate live for the length of the operation. They don’t need to be thread-safe, even though the code is run on a separate thread — because they are accessed *only* on that thread. While they’re working, they know nothing about the outside world, and the outside world knows nothing about them.

1. The SAX parser wrapper knows about the NSData it was initialized with, and it knows it has a delegate.
2. The SAX parser delegate knows about the intermediate objects it’s creating.
3. The intermediate objects don’t know about anything.

So these objects work together, but, importantly, they never use KVO or notifications in any way. Instead they use the delegate pattern (whether via blocks or methods isn’t conceptually important).

The objects work together, but as loosely as possible while still keeping the group isolated to its task.

In the end, only the intermediate objects survive — they’re passed to the main thread, where they’re used to update the model. And then they’re discarded.

#### Worst-Case Scenario

I’ve used the phrase “update the model” several times and mentioned doing it on the main thread. A few years ago I would never have dreamed of that — but computers and devices have gotten so much faster that it’s worth going main-thread-only at first, and considering alternatives only after dealing with everything else that can and should be safely moved to a queue.

You *really* don’t want to update model objects on background threads. It’s a crash-making machine. But testing and profiling may tell you that you need to.

Try to break down the problem. If updating the model is okay *except* for this one thing — something that involves turning NSData into a UIImage or NSImage, for instance — then move *just that slow part* to a background task. (Creating an image from data or a file is a perfectly good thing to move off the main thread. It’s easily isolatable.)

It could be that the problem is the database: perhaps you find that it’s otherwise fast to create objects and update properties in memory, even a whole bunch of them. In that case, you might do what I do, which is de-couple the database calls from the main thread. (It’s not that hard: the database code needs to run on a serial background queue, and it should do everything in the exact some order that things happen in the main thread.)

Which is to say: there are options.

But if you still find that you have to update the model on a background thread, then you just have to do it. Remember that the rest of your app is on the main thread, so when posting notifications and so on, do so on the main thread.

#### Summary

Do everything on the main thread. Don’t even think about queues and background threads. Enjoy paradise!

If, after testing and profiling, you find you do have to move some things to a background queue, pick things that can be perfectly isolated, and make sure they’re perfectly isolated. Use delegates; do not use KVO or notifications.

If, in the end, you still need to do some tricky things — like updating your model on a background queue — remember that the rest of your app is either running on the main thread or is little isolated things that you don’t need to think about while writing this tricky code. Then: be careful, and don’t be optimistic. (Optimists write crashes.)
