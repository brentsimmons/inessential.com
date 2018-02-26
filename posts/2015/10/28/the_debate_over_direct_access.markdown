@title The Debate Over Direct Access
@pubDate 2015-10-28 16:22:11 -0700
@modDate 2015-10-28 16:23:07 -0700
At lunch today a few of us discussed the issue of using `self.foo` vs. `_foo` in Objective-C.

We had people on two sides. I’ll lay out the arguments.

(Note: *this isn’t even a debate* in Swift, which is one of the reasons I’m eager to switch to Swift.)

#### self.foo

This side argues against declaring ivars, and argues that all properties — external and internal — should be synthesized (usually implicitly).

The only cases where you access the underlying storage directly — reference `_foo`, in other words — is in init, dealloc, and in custom accessors. Otherwise you use `self.foo` everywhere.

Reasons:

* It’s a simple rule to remember. You don’t have to remember whether a property is internal or external.

* A given property can have custom accessors, or not, and you still treat it the exact same way. Adding or removing custom accessors does not mean you have to go looking for all the references to that property and possibly change them.

* You’re treating your object’s interface as an API. Inside the object you have more API than outside callers can see, which is fine. It’s still all API.

* You have to worry less about KVO if you always use `self.foo` instead of `_foo`.

* You’re more likely to get memory management right if you use `self.foo`. (This is much less of an issue with ARC, I grant.)

* Subclasses are more likely to get things right if you use `self.foo`.

* Apple seems to advocate this style. (Not always consistently.)

#### _foo

This side argues that using direct storage access inside an object is the way to go.

Reasons:

* There’s a useful distinction between public and private. The code for an object is private, and it’s therefore fair to access storage directly. An object has one API — its public API — and inside the object you can do whatever makes sense.

* Any time you send a message, it’s possible that anything could happen, including reentrancy bugs and so on. Accessing storage directly does not have that problem.

* Sending a message may have performance issues. (Probably not. But it’s possible.)

Okay — I don’t fully understand this side of the argument. I did the best I can to explain it, but I’m most definitely in the `self.foo` camp.

But smart people disagree with me.

Why am I wrong, and why is `_foo` better?

(Feel free to <a href="https://twitter.com/brentsimmons/status/659510667137847296">reply on Twitter</a>, of course.)
