@title A multi-threading rule of thumb
@categoryArray Cocoa-Development
@pubDate Sat Mar 19 14:59:25 -0700 2011
@modDate Sat Mar 19 14:59:25 -0700 2011
One indicator — not the only one — that you’re doing threading right: you should be able to look at any method in your code and know immediately whether it’s main-thread only, single-thread-only, or multiple-threads. (Let’s set “immediately” to 10 seconds just to be reasonable.)

If you find yourself doing a lot of defensive stuff — like “Oh, this might get called by a background thread, maybe, possibly, not sure, so let’s check and do a performSelectorOnMainThread just in case” — then you still have issues.

The same goes for data structures: you should absolutely know which are main-thread-only, single-thread-only, and which need locking. And don’t rely on atomic properties to take care of threading issues — if you’re doing it that way, you’re working at the wrong level.
