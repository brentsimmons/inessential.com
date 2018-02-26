@title How Not to Crash #6: Properties and Accessors
@pubDate 2015-05-27 13:37:24 -0700
@modDate 2015-05-27 14:04:43 -0700
This gives me the willies:

<code>- (void)someRandomMethod {</code><br />
<code>&nbsp;&nbsp;some stuff…</code><br />
<code>&nbsp;&nbsp;\_thing = otherThing;</code><br />
<code>&nbsp;&nbsp;other stuff…</code><br />
<code>}</code>

You could prove that it’s correct. You’re using ARC, so the proper retains and releases are added. And nobody is observing _thing.

Fine. It’s legal and it works.

Say you realize that thing should be observable. So every place you set thing, you bracket the call:

<code>[self willChangeValueForKey:kThingKey];</code><br />
<code>\_thing = otherThing;</code><br />
<code>[self didChangeValueForKey:kThingKey];</code>

Also legal, also works.

The problem is the future: later today, tomorrow, or in six months, you or somebody else writes a custom setter for thing — maybe because you need something like <code>self.needsDisplay = YES</code> when thing is set — and now you have a bug where the view doesn’t redraw whenever thing changes.

Or worse: perhaps that future custom setter tears down an observer and sets up a new one whenever thing changes. Since you’re setting _thing directly, the observations won’t be maintained properly, and you’ll get crashes.

The answer is a simple rule: use the accessor when getting and setting properties.

In other words, do this:

<code>- (void)someRandomMethod {</code><br />
<code>&nbsp;&nbsp;some stuff…</code><br />
<code>&nbsp;&nbsp;self.thing = otherThing;</code><br />
<code>&nbsp;&nbsp;other stuff…</code><br />
<code>}</code>

This works whether or not you have a custom setter. When setting thing, you don’t have to care one way or the other.

(Here’s the simple test of a programming rule: if you can’t go wrong by following it, but you *can* go wrong by *not* following it, then you should follow it.)

(Don’t worry about the performance issue of going through accessors. I’m a performance junkie, and I’ve never seen this become a problem. If your app develops performance issues, profile it and find out the real cause.)

#### Exceptions

You should *not* go through the accessor in four places: init methods, dealloc, custom getter, and custom setter. This avoids side effects.

If you *need* a side effect — removing an observer, for instance, in dealloc — that you’d normally place in the setter, make it a separate method and call it from the setter and from dealloc. (Also consider that adding and removing observers outside of init and dealloc is a possible sign that your code needs refactoring.)

#### Auto-synthesize

Don’t create instance variables, ever. Declare properties instead.

Properties auto-synthesize instance variables. Use @synthesize only when Xcode tells you you need to.

#### Use ARC

And if you have non-ARC code, upgrade it to use ARC. Manual memory management is error-prone. Even someone with years of experience will make mistakes from time to time, and mistakes can cause crashes (or memory leaks or abandoned memory, at best).

Normally I don’t advocate editing working code that’s running fine — but if you have code that needs maintaining, do yourself and your co-workers a favor and convert it to ARC. (*Everybody is going to get worse at manual memory management over time.* And there are no points added for being a hero.)

(It *is* possible to run into performance issues with ARC, particularly if you’re dealing with lots of objects in a loop. Remember to use autorelease pools. And don’t jump to conclusions: use the profiler.)

(Also: the ARC converter may not always do what you want. If you use it, check the changes it makes. Remember that you can convert one file at a time. Targets can have both ARC and non-ARC files.)

#### Don’t do->this

This gives me the screaming meemies: thing->property. No.

#### dealloc

If you don’t need dealloc (since you’re using ARC), then don’t create it. There’s no need to set properties to nil in dealloc.

A big exception is delegates: nil out the delegates.

#### Use weak

Weak is awesome. Delegates, for instance, should be weak.

Parents should retain their children, but children should have a weak reference to their parents (if they have a reference at all). Weak gets you out of those [invalidate methods where you break retain cycles](http://inessential.com/2015/05/14/how_not_to_crash_1_kvo_and_manual_bind).

Do not, under any circumstances whatsoever, use unsafe_unretained. It’s a trap. You might as well do this:

<code>#define CRASHING\_BUG unsafe\_unretained</code>

It’s literally called *unsafe*.

Don’t run with scissors. Heck — don’t even touch these scissors. They have a bunch of poison on them.
