@title On switching away from Core Data
@pubDate Fri Feb 26 15:41:20 -0800 2010
@modDate Fri Feb 26 15:51:52 -0800 2010
A lot of the work I’ve been doing the last several months is optimizing performance for NetNewsWire for iPhone. The changes haven’t shipped yet, because I’m not quite finished. But one part of this might be interesting to other developers, so I figured I’d write it up.

I optimized as much as I could, spent tons of time in Shark, went all multi-threaded with Core Data, switched away from my own queuing system to NSOperationQueue, optimized the XML parsing, etc. But performance and memory use on my first-generation iPod Touch (my development test device) was still not nearly good enough with a big unread count (of around 10,000 items).

At that point, having done everything else, the remaining issue was clearly Core Data. So I tried more things, re-read everything I could about Core Data performance (for the nth time), ran experiments, spent tons more time in Shark. Trying to get it good. No go.

Finally I realized I had to switch away from Core Data and use SQLite more directly. Not completely directly — I use <a href="http://code.google.com/p/flycode/source/browse/trunk/fmdb">FMDB</a>, a lightweight Objective-C interface that works on Macs and iPhones. <a href="http://shapeof.com/">Gus</a> wrote it. It’s good.

That meant a bunch more work — it’s not like Core Data and FMDB are similar or meant to be similar. So it was no drop-in replacement. Not intended to be.

### But why?

I bet Core Data is the right way to go 95% of the time. Or more. It’s easy to work with. It’s fast (in most cases). It has schema upgrade tools.

The important thing to know, though, is that it’s not a database. It’s an object graph and persistence manager. (Check out the <a href="http://cocoawithlove.com/2010/02/differences-between-core-data-and.html">post on Cocoa with Love that goes into detail</a>.)

### But surely you’re using objects

The difference between Core Data and a database was never that clear to me — until I found concrete examples.

After all, under the hood, in the code, every news item in a feed is an object. Why <em>wouldn’t</em> I use an object persistence framework for that? They’re <em>objects</em>, and I want to <em>persist</em> them. Duh. Seems like I should use Core Data.

So here are some concrete examples where direct database access made more sense than using Core Data.

#### 1. Marking lots of news items as read or unread

The app gets from the Google Reader API a big list of item IDs that have been marked read or unread.

In Core Data, I had to loop through the list, change the status for each individual item. The list could be up to 10,000 items long. Not a good idea.

This is a very database-y operation. With one query the app can set the status for a whole bunch of items at once, without having to instantiate them as objects: <code>update newsItems set read = 1 where</code>...

#### 2. Deleting lots of items

Similar to #1 above — from time to time the app deletes old, read, non-starred items from storage. We can’t just let storage grow forever, especially not on an iPhone or iPod Touch.

With Core Data, I ran a query to figure out what items to delete. Then ran a loop that deleted them. Expensive.

With SQLite access, I just did a sinqle query: <code>delete from newsItems where</code>...

#### 3. Dealing with unique IDs from outside system

Core Data does <em>uniquing</em>, but that’s not what this is. The news items have an assigned unique ID that comes from another database.

When refreshing feeds, it’s common to see news items that the app has seen before. They might have been downloaded previously or they might have changed. (We try to avoid the former, of course.)

This means that for each item in a feed, before it’s saved, the app first has to get the existing news item. This is slow. (I tried various techniques: pre-fetching, fetching as needed, fetching only IDs of existing items for a feed, storing existing IDs in a set or dictionary, etc. Nothing helped much. Usually the solution was worse than the original problem.)

Because many thousands of items may come in during a refresh session, and every item has to be checked to see if it exists already, this was a <em>huge</em> performance hit. Better not to do the fetch, right?

With more-direct access, I could just do a <code>insert or replace into newsItems</code>... and it would add the item or replace the existing item. Fast.

#### 4. Testing for the existence of an item

Sometimes the app just needs to know if something exists in the database. With Core Data, it’s a fetch.

With SQLite, here’s one of my favorite tricks: <code>select 1 from someTable where uniqueID = whatever</code>.

In theory it should hit the index only, since it doesn’t actually retrieve anything from the table itself. It’s fast, at any rate.

### My favorite magic

Once I had the above (and everything else) working, there was still more optimization to do.

I had created a set of indexes that I thought would do the trick — but there’s nothing like actually seeing what will happen when a query runs. With direct access, with control over the indexes, I could test and iterate until I got the right set of indexes.

The magic is SQLite’s <a href="http://www.sqlite.org/lang_explain.html">explain query plan</a> command. It tells you what indexes will be used.

### In the end

I didn’t entirely switch away from Core Data. Feeds and folders are still Core Data objects. Since there was no performance gain to be had by switching those over, I left them as-is.

It’s just news items that got switched — but that’s almost all the data.

Making the switch did mean I had to do some things manually that Core Data would have done for me: keeping any in-memory items synced with the database storage, mostly.

But, still, in the end, the new version of the system was less code than the Core Data version. That will not be the case for most apps. I took it as further indication that this was the right move for this particular app.

### Warning

This isn’t about being a hardcore low-level developer or some crap like that. I like Core Data a ton. (I recommend <a href="http://pragprog.com/titles/mzcd/core-data">Marcus Zarra’s book</a>, by the way, which I read twice.) If I could have stuck with Core Data for everything, I would have. (Rule: always work at the highest level possible.)

But how do you know when you might be better off with FMDB or other more-direct SQLite access? I think it goes like this, at least based on my experience:

1. Is performance good? Then stick with Core Data. (That should cover 95% or more of data-driven apps right there.)

2. Is Core Data really the cause of your performance problems? Can you optimize other things? Can you optimize your use of Core Data? Will going multi-threaded do the trick? Try. If you can get performance good, then stick with Core Data.

3. Are your remaining performance problems really database-y things? In other words, are you doing things like setting one or a few properties across a big range of items; deleting lots of items based on a condition; or having to handle unique IDs from another database, and so you’re constantly doing fetches? In other words, can you benefit by <em>not</em> treating your data as objects sometimes? If switching to direct database access won’t help, then stick with Core Data.

My warning: <em>you probably don’t need to switch away from Core Data</em>. It’s the right answer almost every time.

(By the way, were this a Mac app only, Core Data would probably have been fine. But it runs on iPhones too, and that’s where performance optimization becomes so much more critical.)

Anyway: Core Data is the right answer, except when it’s not, and hopefully I’ve made it a little easier to figure out when it’s not the right answer.
