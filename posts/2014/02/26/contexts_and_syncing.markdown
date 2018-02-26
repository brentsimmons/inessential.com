@title Contexts and Syncing
@pubDate 2014-02-26 11:46:19 -0800
@modDate 2014-02-26 11:46:19 -0800
In <a href="http://inessential.com/2013/10/05/vesper_sync_diary_2_core_data">Vesper Sync Diary #2</a> I wrote:

>I set up two <code>NSManagedObject&#8203;Context</code>s: one on the main thread and one with private queue concurrency. The main thread context is the child of the private queue context.

>This way, doing a save on the main thread doesn’t hit the database: changes get saved to the private queue context, which then does a save to the database.

This agrees with <a href="https://twitter.com/drance/status/438556433974456321">Matt Drance’s advice yesterday</a>:

>For ongoing sync, you should consider a private queue parent context w/ main queue as child.

There’s just one thing that worries me about this, and it’s Florian Kugler’s <a href="http://floriankugler.com/blog/2013/4/29/concurrent-core-data-stack-performance-shootout">Performance Shootout</a>, where he found that independent contexts spend far less time on the main thread.

But it should be noted that his performance shootout doesn’t include this particular configuration, with parent as the background context and child as the main thread context.

So… I think that my setup should perform fine. It’s the one Matt suggests. But I’m still at the point where I look at each of my decisions critically.

If you — who have more Core Data experience than I do — know of a good reason *not* to set up my contexts as private/parent and main/child, please <a href="https://twitter.com/brentsimmons">let me know on Twitter</a>.
