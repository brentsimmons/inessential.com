@title The Non-Reactive Solution
@pubDate 2016-04-04 14:22:56 -0700
@modDate 2016-04-04 14:30:47 -0700
<a href="https://sideeffects.xyz/2016/the-reactive-revolution-of-swift/">The Reactive Revolution in Swift</a> intrigued me not only because the solution was different from what I’d normally write but *so was the problem*.

Here is what’s going on (I think):

1. A view controller, part of a chat app, initiates reading data from a socket.

2. The view controller parses that data into a message object.

3. The view controller adds the parsed message to its array of messages. (And, presumably, updates the UI.)

#### The Old-Fashioned Way

The old-fashioned way is presented like this:

On a background queue, load the data and parse it. Then call back to the main thread and update the messages array and the UI.

This is clearly wrong. The author is absolutely right to call this “callback hell” — he’d be right to use stronger language. This is *not* how you do things.

In fact: any time a view controller is making network calls, it’s wrong. Any time a view controller references *any* kind of queues or background threads, it’s wrong. (View controllers — and views — are main-thread-only creatures.)

#### The New-Fashioned Way

The new-fashioned solution, according to the author, is to use Reactive Programming via RxSwift.

I *think*, but I can’t tell for sure, that roughly the same thing is going on. (It’s hard for me to read, which surely can be explained by my not knowing RxSwift. The `addDisposableTo(disposeBag)` part especially worries me, since it looks like a parallel memory management system.)

But let’s set that aside and talk about how I’d solve this problem.

#### How I’d Actually Write It

First thing: the view controller should not be reading data from a socket and parsing the data.

Instead there should be a separate network controller object whose lifetime is not tied to the view controller’s lifetime.

It may be that the view controller needs to tell that network controller to do a thing — such as download more messages — and that’s fine. So give the view controller access to the network controller. A `refresh()` method or whatever.

Ideally, the network controller makes an http call via NSURLSession — this is almost always preferable to sockets. But let’s assume that the server API uses a socket.

So that network controller has a background queue of some kind, which could be a serial queue if needed. Or an NSOperationQueue. Whatever. On that queue it…

1. Loads data from the socket.

2. Parses the data into a JSQMessage object. (JSQMessage is from the original blog post.)

Then, on the main thread, it posts a NewMessage notification meaning that there’s a new JSQMessage.

This way the network controller knows nothing about any view controllers. It knows how to pull data and turn it into an object, and it does so without blocking the main thread.

Yes, you might use GCD, or you might use NSOperationQueue + performSelectorOnMainThread — but, either way, the use of background threads is entirely hidden inside the network controller. The outside world can’t see in and doesn’t know those implementation details.

This way threading issues don’t leak out of the network controller, which is crucially important.

And though you’re potentially using a callback (depending on how you do it) you don’t have to nest them into some kind of hellish situation. It’s minimal, readable, and debuggable.

The chat view controller then needs to do three things:

1. Subscribe to the NewMessage notification.

2. Handle the NewMessage notification by appending to the messages array.

3. Update the UI when the messages array changes.

The second step looks something like this. (Typed into MarsEdit, not actually compiled; might not be completely correct.)

<code>dynamic func newMessage&#8203;DidDownload&#8203;(notification: NSNotification) {</code><br />
<code>&nbsp;&nbsp;if let message: JSQMessage = notification.&#8203;userInfo&#8203;[messageKey] as? JSQMessage {</code><br />
<code>&nbsp;&nbsp;&nbsp;&nbsp;messages = messages + [message]</code><br />
</code>&nbsp;&nbsp;}</code><br />
</code>}</code>

The messages property should have a `didSet` method which calls the thing that updates the UI. This way, any time you change that array, the UI updates.

(In the real world, by the way, it’s probably plural — you don’t handle one new message but potentially many new messages.)

NSNotificationCenter is, I grant, old-school and totally not glamorous. It just plain works, simply and reliably. Among other things, it has the advantage of being a well-known part of the Foundation framework, and you ought to be able to count on every Mac and iOS developer to know how it works and how to use it.

#### No Locks Needed

From the original article:

>Asynchronous programming is not just about running tasks or perform computation in a separate thread, at some point, we will need to synchronize values across threads and the most common solution is to add locks. As soon as locks are introduced, the complexity of the code raises of at least one order of magnitude and one big new component is added to the complexity equation: unpredictability.

There are no locks in the solution I outline above. (I’ve used that general pattern in NetNewsWire, Glassboard, Vesper, and in my two in-development apps — I know it works.)

At most there *might* be a serial queue, but I don’t think I’ve ever used a serial queue with networking. (I do use them for database access, though.)

Here are the tricks: views and view controllers should be main-thread-only. When you have a task in a controller that can block the main thread, make it isolatable and use a background queue of some kind — but <em>keep that implementation detail hidden</em> from the rest of the app. And any networking and parsing must be done in an object whose lifetime isn’t tied to the view controller’s lifetime.

<p style="text-align:center">* * *</p>

I’m *not* saying that Reactive programming is bad, or that RxSwift is bad. I totally don’t know enough to say.

However, there are problems — such as the one the author presents — that have existing solutions that don’t require callback hell, or locks, or tricky-to-understand threading issues.

I don’t think the author intends to misrepresent current best practices — they may just not be as well-known as I think they are. Hence this article.

PS Definitely read Marcus Zarra’s <a href="https://realm.io/news/slug-marcus-zarra-exploring-mvcn-swift/">Exploring MVC-N in Swift</a>. While Marcus and I might implement some details differently, those details are matters of style — in broader terms we are absolutely sitting at the same counter.

PPS I struggled with this article because the last thing I want to do is discourage a developer who’s presumably younger than I am (safe bet) to stop writing. Note to the author: if you’re of a mind to, please write a follow-up! I’ll happily and very gladly link to it.
