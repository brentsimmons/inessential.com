@title Why NetNewsWire Is Fast
@pubDate 2020-05-18 17:14:55 -0700
@modDate 2020-05-18 17:16:22 -0700
NetNewsWire is fast because performance is one of our core values. *Being fast* is part of the very definition of the app.

I suspect that it’s hard to do this any other way. If you take a month or two to speed things up, from time to time, your app will always be — at best — just kind of heading toward satisfactory, but never to arrive.

The best general advice I can give is just this: make sure performance is part of the foundation of your app. Make sure it‘s part of every decision every day.

Make sure, in other words, that performance isn’t just a topping — it’s the pizza.

Below are some of the specific reasons NetNewsWire is fast. Because NetNewsWire is — like many apps these days — basically a fancy database browser where data comes from the web, some of these will apply to other apps.

The below items are in no particular order.

#### Fast RSS and Atom Parsing

The most painful way to parse XML is with a SAX parser — but it’s also how you’ll get the best performance and use the least memory. So we use SAX in our [RSParser framework](https://github.com/Ranchero-Software/RSParser).

On my 2012 iMac, parsing a local copy of some past instance of the Daring Fireball Atom feed — relatively large at 112K in size — happens in 0.009 seconds.

That’s fast, but we do another thing as well: run the parser in the background on a serial queue. Since parsing is a self-contained operation — we input some data and get back objects — there are no threading issues.

#### Conditional GET and Content Hashes

The parsers are fast — but we also do our best to skip parsing entirely when we can. There are two ways we do that.

We use [conditional GET](https://fishbowl.pastiche.org/2002/10/21/http_conditional_get_for_rss_hackers), which gives the server the chance to respond with a 304 Not Modified, and no content, when a feed hasn’t changed since the last time we asked for it. We skip parsing in this case, obviously.

We also create a hash of the raw feed content whenever we download a feed. If the hash matches the hash from the last time, then we know the content hasn’t been modified, and we skip parsing.

#### Serial Queues

The parser isn’t the only code we run on a serial queue. When an operation can be made self-contained — when it can just do a thing and then call back to the main thread, without threading issues — we use a serial queue if there’s any chance it could noticeably block the main thread.

The key is, of course, making sure your operations are in fact self-contained. They shouldn’t trigger KVO or other kinds of notifications as they do their work.

(A simple example of a background thing, besides feed parsing, is creating thumbnails of feed icons.)

#### We Avoid the Single-Change-Plus-Notifications Trap

Here’s an example of a trap that’s easy to fall into. Say a user is marking an article as read. Calling `article.read = true` triggers, via KVO or notifications or something, things like database updates, user interface updates, unread count updating, undo stack maintenance, etc.

Now say you’re marking all articles in the current timeline as read. You could call `article.read = true` for each article — and, for each article, trigger a whole bunch of work. This can be very, very slow.

We have specific APIs for actions like this, and those APIs expect a collection of objects. The same API that marks a single article as read is used to mark 10,000 articles as read. This way the database is updated once, the unread counts are updated once, and we push just one action on the undo stack.

#### Coalescing

We also try to coalesce other kinds of work. For instance, during a refresh, the app could recalculate the unread count on every single change — but this could mean a ton of work.

So, instead, we coalesce these — we make it so that recalculating unread counts happens not more often than once every 0.25 seconds (for instance). This can make a huge difference.

#### Custom Database

For an app that is, again, just a fancy database browser, this is where the whole thing can be won or lost.

While Core Data is great, we use SQLite more directly, via [FMDB](https://github.com/ccgus/fmdb), because this gives us the ability to treat our database as a database. We can optimize our schema, indexes, and queries in ways that are outside the scope of Core Data. (Remember that Core Data manages a graph of objects: it’s not a database.)

We use various tools — such as [EXPLAIN QUERY PLAN](https://sqlite.org/eqp.html) — to make sure we’ve made fetching, counting, and updating fast and efficient.

We do our own caching. We run the database on a serial queue so we don’t block the main thread. We use structs instead of classes, as much as possible, for model objects. (Not sure that matters to performance: we just happen to like structs.)

To make searching fast, we use SQLite’s [Full Text Search extension](https://www.sqlite.org/fts5.html).

I could, and probably should, write more articles going into details here. The database work, more than anything else, is why NetNewsWire is fast.

#### Sets and Dictionaries

We often need to look up things — a feed, given its feedID, for instance — and so we use dictionaries frequently. This is quite common in Mac and iOS programming.

What I suspect is less common is use of *sets*. The set is our default collection type — we never want to check to see if an array contains something, and we never want to deal with duplicate objects. These can be performance-killers.

We use arrays when some API requires an array or when we need an ordered collection (usually for the UI).

#### Profiler

Instead of guessing at what’s slow, we use the profiler in Instruments to find out exactly what’s slow.

The profiler is often surprising! Here’s one thing we found that we didn’t expect: hashing some of our objects was, at one point, pretty slow.

Because we use sets quite a lot, there’s a whole lot of hashing going on. We were using synthesized equality and hashability on some objects with lots of string properties — and, it turns out, hashing strings is pretty darn slow.

So, instead, we wrote our own hash function for these objects. In many cases we could hash just one string property — an article ID, for instance — instead of five or ten or more.

#### No Stack Views

My experience with stack views tells me that they’re excruciatingly slow. They’re just not allowed.

#### No Auto Layout in Table Cell Views

When people praise a timeline-based app like NetNewsWire, they often say something like “It scrolls like butter!” (I imagine butter as not actually scrolling well *at all*, but, yes, I get that butter is smooth.)

While we use Auto Layout plenty — it’s cool, and we like it — we don’t allow it inside table cell views. Instead, we write our own layout code.

This is not actually difficult. Maybe a little tedious, but laying out a table cell view is pretty easy, really.

I figure that optimized manual layout code is always going to be faster than a constraint solver, and that gives us an edge in smooth scrolling — and this is one of the places where an otherwise good app can fall on its face.

And: because that layout code doesn’t need a view (just an article object and a width), we can run it at any time. We use that same code to determine the height of rows without having to run an Auto Layout pass.

#### Caching String Sizes

Text measurement is slow — slow enough to make even manual layout too slow. In NetNewsWire we do some smart things with [caching text measurement](https://inessential.com/2019/07/26/a_couple_handy_tricks_for_text_measureme).

For example: if we know that a given string is 20pts tall when the available width is 100 and when the available width is 200, we can tell, without measuring, that it will be 20pts tall when the available width is 150.

#### Summary

There’s no silver bullet. Making an app fast means doing a bunch of different things — and it means paying attention to performance continuously. 🍕
