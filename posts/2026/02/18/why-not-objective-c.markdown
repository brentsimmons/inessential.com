@title Why Not Objective-C
@pubDate 2026-02-18 15:00:00 -0800

At my last job, at Audible (hi Audible folks, if you’re reading this!), I led the effort to port our remaining Objective-C to Swift. When I started that project, Objective-C was about 25% of the code; when I retired it was in the low single digits (and has gone even lower since, I’ve heard).

Why do this? It was working code! Don’t we all know not to rewrite working code?

### Why get rid of Objective-C

Well, we knew a few things: one was that our Objective-C code was where a lot of our crashing bugs and *future* crashing bugs (and bugs of all kinds) lived.

So it was working code, yes, but we knew there were crashes hidden in there, and that some of those crashes were ambush hunters, playing the long game, waiting for years before pouncing. Best just to rewrite it all in Swift, the safer language.

A second thing we knew was that having to interoperate between Swift and Objective-C is a huge pain. It often means dumbing-down the Swift code and not using modern features, which limited our options for good Swift code.

And a third thing we knew was that very few of our engineers had a background writing Objective-C. Maintaining that code — fixing bugs, adding features — was more expensive than it was for Swift code. (Duh, right? When you have many engineers working on a project, it’s best if the language you use is one everybody knows well.)

### Not that this went perfectly

This is still risky, by the way. Rewriting code is always risky.

At one point I was responsible for a bug where we sent an integer to some API and it should have been a boolean — because the original code was using NSNumber and it wasn’t obvious which it should be. This caused a partial outage of push notifications, which I estimated (very roughly) to have cost the company a few hundred thousand dollars.

(Really? A little bug like this? NS-fucking-Number cost all this money? Yes. Audible scale may not be Facebook scale, but it’s far beyond the scale of indie apps. Before Audible I always worked for smaller companies with smaller audiences — working on something with many millions of users was enlightening and terrifying.)

But here’s the thing: this proved my point. Someone trying to maintain that code as Objective-C might have easily made the same mistake and caused the same outage. The Swift code we replaced it with is type-safe: it’s unmistakably and clearly a boolean and not an integer (once we fixed it; other way around at first). Replacing Objective-C code with Swift is clearly a win.

### Goodbye to all those square brackets

I didn’t count how many hundreds of thousands of lines of Objective-C my project was responsible for rewriting (and sometimes just deleting). It was a lot. Multiple entire apps could fit in those lines-of-code counts.

And if you look at [NetNewsWire’s code](https://github.com/Ranchero-Software/NetNewsWire), you see that it’s almost entirely Swift, with just a little Objective-C for the various parsers and FMDB. It’s not just a Swift app but a modern Swift app that uses async await and structured concurrency. (Mostly modern — there’s still some code to update to async await. Work continues.)

I say all of the above to show that I’m not stuck in the old ways; I’m not the guy insisting on the supremacy of Objective-C despite the obvious evidence against. I’m the guy who got rid of Objective-C — with glee and (oops, sorry Audible marketing team for the screwup) wild abandon!

I want you to know all the above in advance because in my next post I’m going to talk about how I wrote some new code in Objective-C and loved it.
