@title More Coding Nits
@pubDate 2014-05-03 15:24:39 -0700
@modDate 2014-05-03 15:52:38 -0700
I’m looking at a project on GitHub. I’m not going to name it, because it’s not my thing to embarass anyone.

But I’ll take the opportunity to point out some things I noticed.

* Accessors shouldn’t be of the form `getSomething`. Drop the `get`.

* <code>#define SOME_CONSTANT 10</code> isn’t Cocoa-like. Better is <code>static const NSUInteger PBSSomeConstant = 10;</code> (Where PBS is replaced with your prefix.)

* If you’re calling something a Handle, it should be an actual Mac memory Handle. And we shouldn’t be using Handles anymore.

* All of your class names should have a prefix. All of them.

* Header files should expose only what’s needed by the outside world. Use class extensions to keep private things private.

* If you’re jumping through hoops to create a cancelable block, consider an `NSOperation` instead. Or <code>performSelector:&#8203;withObject:&#8203;afterDelay:</code> combined with <code>cancelPrevious&#8203;PerformRequests&#8203;WithTarget:&#8203;selector:&#8203;object:</code>. Or an NSTimer.

* Don’t over-comment. No need to say a line is creating a `UILabel`, for instance, when it’s obvious. Comments are for illumination and are sometimes necessary — but, in general, you should write code that needs no illumination.

* The `init` method should return `instancetype` and not anything else. (Or `id` if you’re supporting older OSes.)

* You shouldn’t use self.whatever accessors in `init`, except when unavoidable. Use _whatever instead. (Same thing in `dealloc` and in custom accessors.)

* Turn on more errors and warnings. (Even consider treat-warnings-as-errors.) [Peter Hosey’s list is good](https://github.com/boredzo/Warnings-xcconfig/wiki/Warnings-Explained). It makes your code better — and it means that if someone else uses your code they don’t have to go through and fix things.

* If your code is meant for iOS 7 or Mac OS 10.9, use @import.

* If you register for notifications, and there’s any code path where you might not call `removeObserver`, fix it.

My point, by the way, is *not* to make anyone afraid of releasing their code. Don’t be afraid — releasing code is a great thing to do.

I’ve released dumb stuff sometimes. Totally idiotic things. It’s fine. The point is to learn and get better. That’s it.
