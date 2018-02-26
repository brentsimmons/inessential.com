@title On Coalescing Calls
@link http://www.getitdownonpaper.com/blog/2013/01/03/coalescing/
@pubDate Thu Jan 03 21:11:42 -0800 2013
@modDate Thu Jan 03 21:24:24 -0800 2013
Doug Russell writes about <a href="http://www.getitdownonpaper.com/blog/2013/01/03/coalescing/">using performSelector:withObject:afterDelay:</a> to coalesce multiple calls into one.

I’ve done similar coalescing, but by using an NSTimer. I haven’t gone to the trouble of writing a category for this (but I should). Here’s what I do:

1. Create a method like <code>scheduleReloadData</code>.

2. In that method, I create a timer that fires soon (like in .2 seconds). If a timer already exists, I invalidate it and release it.

3. When the timer fires, it calls a method like <code>reloadTimerDidFire:(NSTimer *)timer</code>. In that method I get rid of the timer and actually call <code>reloadData</code>.

I think my method would coalesce calls over a longer period than Doug’s method — but at a cost, of course. (Latency, for one thing.)

This reminds me of another form of coalescing I’ve used a little bit, but that doesn’t seem to be common (as far as I can tell): <a href="http://developer.apple.com/library/ios/#documentation/cocoa/reference/foundation/Classes/NSNotificationQueue_Class/Reference/Reference.html">NSNotificationQueue</a>.

You can coalesce multiple notifications into one, and choose how they’re coalesced (end of the run loop or until the run loop is idle).

I haven’t found NSNotificationQueue to be massively useful — but it’s occasionally useful. File under Cocoa nooks and crannies.

<i>Update a few minutes later:</i> I totally missed Doug’s note at the end about using an interval greater than 0.0 to coalesce calls over a longer period. That should do the trick to replace my timer-based method.
