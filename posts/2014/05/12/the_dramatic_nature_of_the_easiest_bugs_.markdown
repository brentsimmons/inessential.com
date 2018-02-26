@title The Dramatic Nature of the Easiest Bugs to Fix
@pubDate 2014-05-12 17:02:31 -0700
@modDate 2014-05-12 17:08:22 -0700
When I first started out as a software developer I assumed that the worse the effect of a bug, the harder it would be to fix. Seems obvious, right? I’d bet the average non-programmer assumes this. It’s intuitive.

I learned quickly, though, that there was no relationship at all between the severity of the effects and the difficulty of the fix.

A crashing bug, after all, could be just because you didn’t add a : character when you needed one. That’s not even a one-line fix — it’s a one-character fix. While a crashing bug is highly dramatic, the fix is often very simple.

I had a bug the other day where a table view was empty when I knew it should be full of data. Definitely dramatic. What’s gone wrong? Is the data layer totally fubar? Do I need a complete rewrite?

Nah — I’d forgotten a ! character in one line in the view controller. Whew.

But then there was this other bug, a UI glitch. It was annoying — obviously wrong — but not at all dramatic. Just wrong. Looked like a quick fix — but it wasn’t. It took hours.

After all these years I’ve come around to this thought: the apparent severity of a bug is in inverse proportion to how hard it is to fix.

(Side note. Question. Why do people sometimes say that an app crashed *hard*? The app stopped running abruptly. It’s not a crash otherwise. What makes a crash a <em>hard</em> crash?)

#### Counter-examples

Consider the situation where you have an intermittent crashing bug because you haven’t quite figured out mutability and concurrency and your data layer is, in fact, not good. Then you’d have a dramatic bug (crashing) that’s also difficult to fix (maybe rewriting the data layer).

Or consider the situation where you’re relying on something else that’s crashy. I had a Mac app years ago that used to crash mainly because of WebKit and Flash bugs. (Mostly Flash. Ugh.)

There was nothing I could do about these crashes. They weren’t even fixable (by me) at all.

#### Revised Observation

Perhaps this makes more sense:

Given a programmer who’s good at their job — who knows the language, frameworks, and runtime well — the dramatic nature of a bug is in inverse proportion to the difficulty of the fix as long as the bug is actually in that programmer’s code.

And that sounds pretty good. Except that there are cases where something is off by one pixel and fixing it is super-simple. So some non-dramatic bugs are also easy to fix, which means this revised observation still isn’t true.

But then there <em>are</em> times when something is off by one pixel — [or three](http://www.cabel.name/2007/09/coda-toolbar-and-three-pixel-conundrum.html) — and there’s absolutely nothing you can do since the frameworks won’t let you. (Nothing you can do short of going [partial or full Brichter](http://www.macstories.net/featured/a-conversation-with-loren-brichter/), that is.)

So now, as much as I wanted to make a nice and true observation, I’m left with this:

The more dramatic the bug, the easier it is to fix. 90% of the time. Well, 75% of the time. Well, half the time.

Or, who really knows. [Programming sucks](http://stilldrinking.org/programming-sucks).
