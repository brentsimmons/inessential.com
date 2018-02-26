@title UIGestureRecognizer and nil-targeted Actions
@pubDate Fri Jun 22 17:14:22 -0700 2012
@modDate Sat Jun 23 12:09:56 -0700 2012
I like the Cocoa responder chain — I like being able to specify <code>nil</code> as target and have the action message follow the responder chain until it’s handled (or not).

I like this so much I almost never specify a target — I (just about) always use <code>nil</code>.

But this doesn’t work with <code>UIGestureRecognizer</code>. The <a href="http://developer.apple.com/library/ios/#documentation/UIKit/Reference/UIGestureRecognizer_Class/Reference/Reference.html">documentation states</a> that “nil is not a valid value” for the target in <code>addTarget:action:</code>.

If I forget and use nil anyway, nothing happens. (Which is frustrating, because I don’t know why until I remember or look it up. Which just happened.)

How I work around it:

I specify the target in the same file where the gesture recognizer is created. I have it call a method something like this:

<script src="https://gist.github.com/2975787.js?file=gistfile1.txt"></script>

<code>rs_performSelectorViaResponderChain</code> looks like this:

<script src="https://gist.github.com/2975795.js?file=gistfile1.m"></script>

I don’t like having to do this, but it works.

#### Why oh why

But my question is: why does UIGestureRecognizer not take nil as a target and work like everything else works?

I don’t have a theory.

<i>Update 10:30 pm:</i> <a href="https://twitter.com/ctp/status/216399589945782272">Chris Parker writes on Twitter</a>:

“They’re intended for specific gestures on views, rather than a hierarchy of actions. More of a virtual control.”

<i>Update June 23, 2012 12:00 pm:</i> Ben Lings <a href="https://twitter.com/ben_lings/status/216554426767392768">asked on Twitter</a> why I didn’t use <code>-[UIApplication sendAction:to:from:forEvent:]</code> instead of <code>rs_performSelectorViaResponderChain</code>.

Excellent question. I think I <i>should</i> be using <code>sendAction:to:from:forEvent:</code>. So I changed my code.
