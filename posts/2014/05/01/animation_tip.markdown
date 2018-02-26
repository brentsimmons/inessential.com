@title Animation Tip
@pubDate 2014-05-01 20:48:03 -0700
@modDate 2014-05-01 21:14:07 -0700
I had some circles to animate. I’ve been living in server-side land and database land for months — but here I am back to the normal world where we jiggle stuff for a living.

(I want that on a T-shirt. “I jiggle stuff for a living.”)

These circles start out small and get bigger, then small again, then bigger.

So I made them at the normal size and did the transform scale thing to make them bigger — and they were blurry. Blurry little jigglers.

So I did what I always do — which is to go into a tailspin of research (and loathing of computers, this industry, and everybody who was born since 1800). (Well, I went to StackOverflow, like everybody else does. I’m not weird.)

Nothing leapt out at me. Is there anything I can do to make them not-blurry when they get bigger?

The answer, finally, was so simple: draw them big first, and do the transform scale thing to make them small. It doesn’t actually matter that they’re shown as small first — they can still be drawn big.

Problem solved. I take back all the cursing. Sorry.

<p style="text-align:center">* * *</p>

The truth is that it probably wouldn’t have mattered. On the big simulator the blurriness popped out at me, but on the device it probably wouldn’t have been noticeable. But <em>I</em> would have known, and that matters.

<i>Update 9:10 pm</i>: There’s an even better way to do this: animate a CAShapeLayer. [Alex Novosad pointed](https://twitter.com/AlexDaUkrainian/status/462079616442576896) me to this [answer on StackOverflow](http://stackoverflow.com/questions/10809280/drawrect-circle-and-animate-size-color) which shows how to do it.

Confession: I constantly forget about Core Animation. I need more experience there, for sure.
