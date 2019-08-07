@title Vesper Sync Diary #2 - Core Data
@pubDate Sat Oct 05 14:42:57 -0700 2013
@modDate Sat Oct 05 15:00:41 -0700 2013
I figured I should take a look at <a href="http://vesperapp.co/">Vesper</a>’s database layer and make any needed changes there first, before writing syncing code.

So last weekend I switched from SQLite/FMDB to Core Data. This may <a href="/2010/02/26/on_switching_away_from_core_data">come as a surprise</a>.

Here’s what happened. I was adding support for multiple attachments per note (I’m not promising it as a feature, but I need to code for it) and I found myself setting up yet another lookup table to handle the to-many relationship. My code was getting more complex and less easy to maintain.

Core Data is famously good at handling relationships. I found myself wishing I could just use Core Data rather than have to do this manually again.

#### NSFetchedResults&#8203;Controller

Meanwhile, in the back of my head was this small <code>UITableView&#8203;Delegate</code> addition in iOS 7:

<code>- (CGFloat)tableView:&#8203;(UITableView \*)&#8203;tableView estimatedHeight&#8203;ForRow&#8203;AtIndexPath:&#8203;(NSIndexPath \*)path;</code>

The great thing about <code>NSFetchedResults&#8203;Controller</code> is that it loads objects in batches — but for tables with variable row heights, where you need to load each object in order to calculate each row height, batching was defeated. You needed to load all the objects in order to calculate all the row heights.

With <code>estimatedHeight&#8203;ForRow&#8203;AtIndexPath</code> I can now use that (very nice) batching system, and just estimate row heights for unloaded objects. The row heights can be calculated as rows are about to be displayed, and not before. (I also keep an in-memory cache keyed to each object’s uniqueID.)

Suddenly <code>NSFetchedResults&#8203;Controller</code> was made *useful*.

That tipped the scales for me. I decided to take the weekend and do a Core Data implementation for the database layer, and just back out if I get spooked.

#### I Didn’t Get Spooked

I decided going in that I’d do things the straightforward way. No premature optimization. And this meant the scariest thing of all: I would allow database access on the main thread. (For fetches and faulting-in objects.)

I was startled by how fast it was. (On my iPhone 5. I haven’t upgraded, but it hasn’t escaped me that it should be even faster on the new iPhones.) And this reminded me that the last time I worked with Core Data on iPhones was in 2010. Devices have come a *long* way since then. This was good news.

I did make one exception to the do-it-straightforwardly rule. I set up two <code>NSManagedObject&#8203;Context</code>s: one on the main thread and one with private queue concurrency. The main thread context is the child of the private queue context.

This way, doing a save on the main thread doesn’t hit the database: changes get saved to the private queue context, which then does a save to the database.

I am otherwise — so far, anyway — not doing multi-threaded Core Data. Which is awesome, because once you start doing that it’s just about time to switch away. (Core Data is beautiful as an intelligent persistence layer that you work with on the main thread. Once you go multi-threaded, it’s just a weird database system.)

#### I Could Still Throw All This Work Away

I have no doubt that Core Data is up to just about anything a consumer app would do on a Mac. But iPhones are not Macs.

I still need to run some tests. With Vesper’s FMDB/SQLite database system, I tested it by importing Daring Fireball’s Linked List archive and Dave’s tweets. (Up through early 2013.) This was about 30,000 notes and thousands of tags. It took some work, but I got it fast enough to handle this amount of data easily.

I don’t know yet how Core Data will handle this. It may handle it just fine. Or it may be that I need to do some performance work.

The worst-case scenario is that Core Data can’t handle it and no amount of performance work on my part can fix it. (Or, alternately, the necessary performance optimizations make the code too complex and too hard to maintain.)

I’m optimistic, but I’ll have to see. (If you hear nothing more from me about this, you can assume it worked out.)

#### Lesson Learned

Vesper is exactly the kind of app Core Data was meant for: it’s an object graph. Notes, tags, and attachments.

Now, were I writing an RSS reader (I’m not), I still wouldn’t use Core Data. The thing that took me away from Core Data years ago still applies: there are times when you need to mark 10,000 items (or whatever) as read all at once, and loading all of those via Core Data just to flip a property is *not* an option. Not even in a background thread. (Then there’s also the deleting problem, which is similar. You can’t let the database grow forever — you want to delete old articles periodically. That should be one SQL call; it shouldn’t mean loading in a ton of managed objects just to delete them.)

(This would probably be true were I writing a Twitter or ADN client, too. Which I’m also not doing.)

Anyway. Core Data. Even though I’ve talked about how I don’t use it, I’ve always said that *you* should use it, because it’s the right thing in 95% of cases. And Vesper is one of those cases.

Well. Pending my performance tests, that is.

PS I should add that I’m not using Core Data for images. Thumbnails are managed via FMDB/SQLite, and full-size images are stored as separate files on disk. I have no reason to make changes with image-handling.
