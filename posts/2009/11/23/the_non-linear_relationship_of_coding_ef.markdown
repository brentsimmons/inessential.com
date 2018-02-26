@title The non-linear relationship of coding effort and results
@pubDate Mon Nov 23 12:26:55 -0800 2009
@modDate Mon Nov 23 12:26:55 -0800 2009
This is counter-intuitive, so I don’t think most users of software understand it.

Picture a situation like this: an app crashes every time you click a certain button. What does that say?

Well, a crash is a very bad thing, so it probably means a great deal of effort to fix it. It seems like there should be a relationship between the badness of a result and the time it would take to fix it.

But there isn’t. Not necessarily, at least.

A crash can be the simple result of a single missing or mis-placed character. (A very embarrassing crash in NetNewsWire 3.2 was the result of a missing :. I think 3.2.1 differed from 3.2 only in that it added that : at the right place.)

There’s another level of non-linearity: just because a fix is really, really, easy to implement (such as just adding a : at the right place) doesn’t mean the level of effort is small. It may take a week to find exactly what the problem is. Once figured out, it may take 3 seconds to fix it.

Or... not. It may take only seconds to figure out the problem, and just a few more to fix it. Sometimes a crash log and a peek at the code are <em>all</em> that’s required. Sometimes the worst, most obviously bad results have the quickest find-and-fix time. Sometimes.

<img src="http://inessential.com/images/atom.gif" width="29" height="30" alt="" />

What had me thinking about this was some coding I did over the weekend.

In a new operation (not in the current shipping version), I noted the app was allocating about 100MB of RAM, for something that should never have gone above about 50K or so.

About 10 minutes later I had it down to 4MB.

But I still need to get it down to about 50K — I still need to shave off about 4MB.

If it took 10 minutes to reduce memory usage by 96MB, then — were there a linear relationship — it should take under half a minute, less than 30 seconds, to go the rest of the way.

That’s the way things work in the real world, after all. If you have 100 bags of leaves to carry out to the curb, each bag will take about the same amount of time as the others.

Instead, it will probably take me about two hours, maybe more, to get rid of that last 4MB.

It’s almost as if you carried out 96 bags of leaves easily and quickly, then realized you can’t get those last four bags, even though they’re exactly the same as all the others, <em>without pouring a new driveway first</em>.

Which is crazy, right? If the real world operated like that all the time, we’d go completely nuts.

<img src="http://inessential.com/images/atom.gif" width="29" height="30" alt="" />

Anyway. Enough rambling.

Now it’s time to do a prime number of handstands, then touch all the walls of my office (twice) with the index finger of my left hand, then iron my tinfoil hat, then get back to programming.

Lots to do.
