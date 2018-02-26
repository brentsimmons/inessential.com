@title A Day of Programming
@pubDate 2014-10-16 09:29:47 -0700
@modDate 2014-10-16 09:29:47 -0700
Sometimes days are like this:

Our testers — who are great — report a regression I caused but that I didn’t notice. Why is sub-pixel anti-aliasing not working in this view? The text looks bad. (Note to self: test with a non-retina display before comitting.)

I investigate, and find, to nobody’s surprise, that the culprit is a layer-backed ancestor scroll view. I turn off layer-backing — I just uncheck that particular box.

Then run the app. It’s good to see sub-pixel anti-aliasing back. But look at how things have gone wonky.

Wonky? Let’s be precise: the layout inside outline view cells is incorrect. If I check the box (turn layer-backing back on), then layout is fixed. Uncheck it, and layout is broken.

(This all sounds straightforward, but I’m glossing over a bunch of things I tried and researched. The above is a couple hours of work.)

The wonky view uses auto layout, but it’s not entirely constraint-driven: there’s a manual <code>-layout</code> method. When an ancestor is layer-backed, then that method is called at the appropriate times. When it’s not, then that method *isn’t* called often enough, or not at all the right times.

Or… but it also looks like something else might be moving those views, giving them a zero origin when it shouldn’t be. Exactly as if it’s doing constraint-based layout and not calling the <code>-layout</code> method. Sometimes.

I click around a while, add NSLogs and breakpoints and all the usual things. I can’t figure out what’s happening. I bring in <code>resizeSubviewsWithOldSize:</code> (the old friend). I accidentally introduce an infinite loop at one point.

To reassure myself, I check that checkbox again (turning on layer-backing) — and layout works again as expected.

Time to get pragmatic.

If it *seems* as if those views are sometimes getting laid-out by their constraints, and <code>-layout</code> isn’t getting called, then maybe that’s really what’s happening. So one possible solution is to give all the views their necessary constraints, so that <code>-layout</code> isn’t needed at all.

I tried it. Success! (I think. At least so far.)

And that was a day of work. In the end I don’t know why there was a problem, but I have a solution. I should probably file a Radar, but it seems like exactly the kind of thing that will be hard to duplicate in a simple case (though I could be wrong).

There’s nothing wrong with days like that. In the end the thing is solvable. What worries me is when I have too many days like that strung together, when I have too many Radars to file.
