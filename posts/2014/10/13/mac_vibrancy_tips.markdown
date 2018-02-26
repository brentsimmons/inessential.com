@title Mac Vibrancy Tips
@pubDate 2014-10-13 10:24:51 -0700
@modDate 2014-10-13 10:24:51 -0700
For one of my projects I’m working with NSVisualEffectView and behind-window blending.

I’ve found a few things that could help people doing the same thing:

* Reminder: don’t forget that its subview should respond YES to <code>allowsVibrancy</code>.

* If it’s in an NSSplitView, make sure the NSSplitView is not layer-backed. <a href="rdar://18585148">rdar://18585148</a>

* Make sure the effect view’s superview is not the first layer-backed view. <a href="rdar://18587102">rdar://18587102</a>

There may be other gotchas, of course, but these are what I’ve found so far.
