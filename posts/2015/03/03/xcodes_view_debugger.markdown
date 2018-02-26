@title Xcode’s View Debugger
@pubDate 2015-03-03 10:24:25 -0800
@modDate 2015-03-04 15:38:20 -0800
At Omni I work on existing apps with large code bases that use a bunch of frameworks. Say I want to make a UI change. I don’t know where to look. Is it implemented in the app or in a framework? Which one? What’s the class I’m looking for?

I can make some guesses, of course, and I could hunt around, and I could ask people.

But it occurred to me (on day one, thankfully) that I could just use Xcode’s view debugger. Build and run the app, click on the Cyberman icon, and select the thing I want to change. Xcode tells me what class it is, and I know right where to go. This has saved me a ton of time.

I’ve used the view debugger for some actual view debugging too, and while it’s pretty good, there are some additional things I wish it did.

It doesn’t tell me if a view has a layer or if it’s opaque or not. What I’d most like is the ability to click a pixel and have it tell me who drew it. (I realize this might be tricky.)

Or, failing that, at least make it easy to print the description for an object. (Yes, I realize that I can do <code>po (id)(0x618000126400)</code> — it’s just that it seems like an obvious place for a shortcut.)

<i>Update 11:00 am</i>: I didn’t know about <code>-[NSView _subtreeDescription]</code>. Very helpful. Does a bunch of what I want.
