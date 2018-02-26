@title dispatch_once
@pubDate 2015-03-05 14:34:15 -0800
@modDate 2015-03-05 14:36:14 -0800
I’ve been doing this for years when I have a static thing and I want to set its value once:

<code>static MyThing *foo = nil;</code><br />
<code>static dispatch\_once\_t onceToken;</code><br />
<code>dispatch\_once(&onceToken, ^{</code><br />
<code>&nbsp;&nbsp;foo = [some thing];</code><br />
<code>});</code>

But lately I’ve been doing this:

<code>static MyThing *foo = nil;</code><br />
<code>if (!foo) {</code><br />
<code>&nbsp;&nbsp;foo = [some thing];</code><br />
<code>}</code>

The advantage of <code>dispatch\_once</code> is that it’s thread-safe — it’s one less thing to worry about when worrying about concurrency.

But here’s the thing: almost all of the code I write runs on the main thread only. And, furthermore, when I use this pattern it’s almost always in UI code (which is main thread code). (For example: initializing a gradient that won’t change and should be kept in memory.)

So <code>dispatch\_once</code> isn’t valuable in those cases. And, worse, it could hide bugs. (If my main thread code *isn’t* running on the main thread, I need to see some problems as a result.)

I’ll keep using <code>dispatch\_once</code> in the ever-more-rare cases where concurrency is actually an issue — but, where it’s not, I’m back to the old-fashioned way.

And the old-fashioned way is less code and easier to read, which I don’t mind at all.
