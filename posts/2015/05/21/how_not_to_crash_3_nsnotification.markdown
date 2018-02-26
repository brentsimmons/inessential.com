@title How Not to Crash #3: NSNotification
@pubDate 2015-05-21 14:36:06 -0700
@modDate 2015-05-21 14:36:06 -0700
In general, I prefer NSNotification to KVO and (especially) to bindings. I do use KVO sometimes — there are times when it’s the most sensible thing. But NSNotification, like many older APIs, is easier to use without crashing.

But you still need to be careful.

#### The One Way to Crash

When an object registers for a notification, and then is deallocated without unregistering, then the app will crash if that notification is posted. That’s the thing you need to avoid. The rest of this article describes how to do that.

#### The Big Rule

I have one simple, hard-and-fast rule: NSNotifications are posted *on the main thread only*. No exceptions. If some code is running in another thread and it needs to post a notification, it does so on the main thread.

This avoids all problems with notifications coming in on threads you don’t expect. It avoids race conditions with unregistering for notifications.

Almost all of an app’s code should be written to run on the main thread. Code that runs in an NSOperation or GCD queue should be isolated from everything else, and should use a delegate pattern (with or without blocks) when multiple objects work together.

Ensuring that notifications are always posted on the main thread ought to be *easy*. (I’ll do another how-not-to-crash article on threading and queues that goes into more detail.)

#### Blanket Unregistering

Some people like the extra housekeeping work of unregistering for each NSNotification explicitly in `dealloc`. You get things like this:

<code>[[NSNotificationCenter defaultCenter] removeObserver:self name:kSomeNotificationName object:someObject];</code><br />
<code>[[NSNotificationCenter defaultCenter] removeObserver:self name:kSomeOtherNotificationName object:someOtherObject];</code><br />
<code>etc...</code>

You can prove when you write this that it’s correct. But it’s not enough to think of a snapshot of your code — you have to think about your code as it moves through time.

And future you or future somebody else might add another notification, and not remember to call `removeObserver` for that specific notification. And then there’s a crash.

The other problem is that future coder may have to go through your code and do an audit to make sure each registered observation is removed. This is a pain: it’s manual and error-prone.

Instead, always do this:

<code>[[NSNotificationCenter defaultCenter] removeObserver:self];</code>

It’s what Indiana Jones would do.

#### Beware Double Registrations

If an object registers for a notification, and then registers for it again, the notification handler will get called twice. There’s no automatic coalescing.

(This used to happen in the old days on iOS a lot with `viewDidLoad`. People would put registration code there — but remember that views could get unloaded and reloaded, which meant multiple registrations for the same notification.)

Your notification handlers should be written so that they can deal with getting called twice. And it should be impossible for a given object to register twice for the same notification. Both.

#### Register in init, unregister in dealloc

In almost every single case, I register for observations in an init method and remove observations in `dealloc`. If I find that an object needs to add and remove observations during the lifetime of the object, then I consider it a strong code smell.

There’s a good chance that 1) either it doesn’t really need to do that, or 2) the object should be split into smaller objects.

You know that an init method will be called just once for a given object. You know that dealloc will be called just once when there are no other references to that object. You can use this knowledge to balance out registering and unregistering without having to think about it or keep track of it. So easy.

#### Avoid addObserverForName

Some people like <code>-[NSNotificationCenter addObserverForName:&#8203;object:&#8203;queue:&#8203;usingBlock:]</code>. It feels modern because it’s block-based, and we all love blocks. (I sure do.)

But it’s a bad idea. You may have saved yourself writing a notification handler method, but you’ve made your housekeeping worse because now you have an extra object to keep around and do a `removeObserver:` on later. That means no blanket unregistering; it means you’re back to doing audits; it means you have another thing to get right.

You might like that the block-based version means you can keep the registration and the notification handler together — but the cost is too high in housekeeping and potential crashes.
