@title Swift Diary #8: forwardInvocation
@pubDate 2015-08-04 13:16:36 -0700
@modDate 2015-08-04 14:14:50 -0700
Let’s say I’m writing an image editor. (I use this example on my blog for historical reasons — because, historically, I like to rib <a href="http://shapeof.com">Gus</a>. It should not be taken as indicative.)

Here’s the problem I’m running into:

I have various layer classes (BitmapLayer, ShapeLayer, GroupLayer, etc.) that live outside the responder chain. There’s a Canvas object that *is* in the responder chain.

So I hook up my menu items and buttons with a nil target and whichever action makes sense.

Now, the Canvas object doesn’t implement the various actions that the layers implement. Instead, the Canvas object implements <code>respondsToSelector:</code> — it returns YES if the selected layer responds to that selector.

And then, if YES, <code>forwardInvocation:</code> in the Canvas object forwards the message to the selected layer.

Well, that’s the design, anyway. Sensible. Time-saving. Simple.

But forwardInvocation and NSInvocation are not available to Swift.

<p style="text-align:center">* * *</p>

But, soft! What light through yonder window breaks!

While <code>forwardInvocation:</code> isn’t available, <code>forwardingTargetForSelector:</code> *is* available.

Which means the Canvas could see if the selected layer responds to that selector, and then does a <code>performSelector:</code> on that layer.

Correct?

If so, then it means that anyone writing an image editor is good-to-go with Swift.

(That last sentence is the rib-Gus part again.)

<p style="text-align:center">* * *</p>

However, Swift support for <code>forwardInvocation:</code> and NSInvocation would be useful. These things have their uses, and while <code>forwardingTargetForSelector:</code> can take care of some of them, they don’t take care of all of them.

<p style="text-align:center">* * *</p>

<b>Update 1:30 pm</b>: Kyle Sluder <a href="https://twitter.com/optshiftk/status/628663380723699712">reminds me</a>:

>Remember that -[NSResponder supplementalTargetForAction:…] does not require its return value to be an instance of UIResponder.

(Or NSResponder, in my case as a Mac app writer.)

At any rate, <code>supplementalTarget&#8203;ForAction&#8203;:sender:</code> might fill the bill even better. The Canvas object could return the selected layer object.
