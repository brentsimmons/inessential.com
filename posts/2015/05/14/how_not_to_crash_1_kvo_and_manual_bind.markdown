@title How Not to Crash #1: KVO and Manual Bindings
@pubDate 2015-05-14 15:20:57 -0700
@modDate 2015-05-14 15:37:30 -0700
I’ve been fixing crashing bugs recently — but rather than write about fixing crashing bugs, I thought it would be more interesting to write about not creating crashing bugs in the first place.

In this first installment I’ll talk about KVO, manual bindings, retain cycles, and invalidate methods.

#### Bindings means never having to say goodbye

iOS developers don’t have this, but Mac folks do: we can bind a property to another property. We can make it so that if x.foo updates, then y.foo updates too.

NSKeyValueBinding.h is in AppKit. Take a look at <code>bind:&#8203;toObject:&#8203;withKeyPath:&#8203;options:</code>

Let’s imagine a button with a title property. That title property should update whenever some controller’s title updates. Let’s say the controller owns that button. You might write code like this:

<code>static NSString *kTitleKey = @"title";</code><br />
<code>[self.button bind:kTitleKey toObject:self withKeyPath:kTitleKey options:nil];</code>

Very convenient, and it works wonderfully.

And you’re well on the road to crashing.

Here’s the problem: the binding retains the <code>toObject</code> object. Which means that the button effectively retains the controller. If the controller retains its button (it should), then there’s a retain cycle. Neither will become zombies, but they could become abandoned.

One way to crash — and this is a true story — is if the abandoned controller listens for a notification (call it BSNotification), and it Does Something when receiving a BSNotification, and when it Does Something it crashes, because it’s no longer conceptually valid and it doesn’t know how to deal with the current state of things.

#### KVO means having to do everything perfectly every time

Let’s add a third object, a model object. What we *really* want is this flow:

modelObject.title changes, which updates controller.title, which updates button.title.

We’ll use KVO this time.

In the controller:

<code>- (NSString \*)title {</code><br />
<code>&nbsp;&nbsp;return self.modelObject.&#8203;title;</code><br />
<code>}</code><br />
<code></code><br />
<code>+ (NSSet \*)keyPaths&#8203;ForValues&#8203;AffectingTitle {</code><br />
<code>&nbsp;&nbsp;return [NSSet setWithObject:&#8203;@"modelObject.title"];</code><br />
<code>}</code>

Okay — now we have the entire flow. When modelObject.title changes, that affects controller.title, and button.title updates with the correct value.

Very convenient, and it works wonderfully.

It will crash, of course, when modelObject is deallocated (because an instance of modelObject was deallocated while it still has an observer).

If, instead, controller is retaining modelObject (as it probably should be), then you have a third object that will be abandoned and never deallocated, and it will sit around stewing and growing eviler by the minute.

#### One way to solve the problem that isn’t that great

The controller could have a method with a name like <code>invalidate</code> that breaks the retain cycles. Once broken, then <code>dealloc</code> will eventually be called for the controller, its button, and its model object.

You might write code like this, which you call when you know for a fact you’re finished with the controller:

<code>- (void)invalidate {</code><br />
<code>&nbsp;&nbsp;[self.button unbind:kTitleKey];</code><br />
<code>&nbsp;&nbsp;self.modelObject = nil;</code><br />
<code>}</code>

Here’s why this solution isn’t great:

Reference counting is a nice solution — it guarantees that when <code>dealloc</code> is called, you know that no object has a strong reference to the object being deallocated. This makes <code>dealloc</code> a great place to remove observations and similar that need removing.

But if you use something like an invalidate method, you’re trying to do the work of reference counting yourself. You *have* to call invalidate, and you have to call it *at the right time*. Can you make that guarantee forever, for every object that has an invalidate method? What if something changes so that more than one object retains the controller? Who calls invalidate, and when?

That’s a lot of extra work and thinking, and part of the goal of programming is to make errors less likely. Relying on invalidate makes errors *more* likely.

#### A better way to solve the problem

Let’s go back to the problem we’re trying to solve:

modelObject.title changes, which updates controller.title, which updates button.title.

Let’s also be clear: controller knows about modelObject and button, but neither of those two know about each other, and neither of those two know about the controller. Here’s how we might handle it without the need for an invalidate method.

In the controller, nuke the custom getter. Nuke <code>keyPaths&#8203;ForValues&#8203;AffectingTitle</code>. Nuke the use of <code>bind:&#8203;toObject:&#8203;withKeyPath:&#8203;options:</code>.

Instead, create a custom setter — because, after all, setters are called when something changes, and the entire problem to solve is propagating changes to a title property.

<code>- (void)setTitle:(NSString \*)title {</code><br />
<code>&nbsp;&nbsp;_title = title;</code><br />
<code>&nbsp;&nbsp;self.button.title = title;</code><br />
<code>}</code>

That solves half the problem: when controller.title changes, button.title changes.

We can’t do something similar with modelObject, since it doesn’t know about the controller. Instead, have the controller observe modelObject.title.

<code>[self.modelObject addObserver:self forKeyPath:&#8203;kTitleKey options:0 context:&#8203;kTitleContext];</code>

Then in the KVO observation method, watch for kTitleContext, then do <code>self.title = self.modelObject.title</code>. This will call the controller’s <code>setTitle:</code> — which then updates button.title.

With this solution there are no retain cycles. There is one line of tear-down work to do, but you can do it in the controller’s <code>dealloc</code> method:

<code>[_modelObject removeObserver:&#8203;self forKeyPath:kTitleKey context:&#8203;kTitleContext];</code>

#### Review and recommendations

The solution we came up with fixes the retain cycle *without* your having to remember to call an invalidate method and call it at the exact right time. It’s safer code.

There’s a good chance it’s less code, too, and it’s more explicit code.

Some recommendations:

Don’t use <code>bind:&#8203;toObject:&#8203;withKeyPath:&#8203;options:</code> ever, in any circumstance. (iOS people: consider yourselves lucky that it’s not an option. Also consider that there’s probably a reason it never made it to iOS.)

Use a custom setter rather than a custom getter when you’re propagating changes. (It’s in the *setter* where a thing changes, after all.)

Avoid invalidate methods in favor of letting reference counting do its thing — because if *you* are the one trying to track references, you’re going to make mistakes. (I realize avoiding invalidate methods isn’t always possible, but it’s probably more possible than you think it is.)

Interlocking observations of any kind make it difficult to think about what happens in your app: it’s better to be explicit whenever it’s reasonable. Once you get enough of these tendrils of observations you’ve built an impenetrable jungle, and making changes becomes scary.

In theory, bindings and KVO are there to promote loose coupling, but in practice the coupling is often just as tight — if not tighter, in a sense — and harder to debug and get right. It’s generally best to do explicit observations (as opposed to <code>keyPaths&#8203;ForValues&#8203;AffectingXyz</code>) and keep your keyPaths free of . characters.
