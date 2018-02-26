@title The Three Keys to iPhone App Performance
@pubDate Thu Apr 26 10:07:47 -0700 2012
@modDate Thu Apr 26 10:07:47 -0700 2012
When I’m writing iPhone code, I keep three things in my mind at all times:

1. Don’t allocate any memory.

2. Don’t do any work.

3. Don’t block the main thread.

Obviously, 1 and 2 are impossible — you’ll need to allocate some memory and the app will actually have to do something. But I bend the stick by thinking of these extreme rules rather than something nicer like “Allocate as little memory as possible” and “Minimize the amount of work the app does.”

(The last one — don’t block the main thread — is totally possible, of course. That rule isn’t extreme at all.)

One example lesson I’ve learned: when you have a complex, variable-height table view cell with a bunch of layout, it can be tempting to want to cache that layout — or at least text and image measurements — so that you can avoid the work of re-measuring and re-laying-out.

I’ve found that *sometimes* that’s actually slower — because, after all, caching and retrieving from a cache also involves memory allocation and work. Caching isn’t free.

And sometimes it’s <em>not</em> slower.

So I’ll add a fourth key:

<strong>Use Instruments.</strong>

Not an extreme rule — a necessity.
