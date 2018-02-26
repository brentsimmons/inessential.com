@title Why “Just Store the App Data on Dropbox” won’t work for RSS readers
@pubDate Tue Oct 25 12:29:04 -0700 2011
@modDate Tue Oct 25 12:34:07 -0700 2011
When I was developing an RSS reader, users often asked me if I would make it sync via Dropbox (or WebDAV or iDisk or similar).

For a while, years ago, before Dropbox existed, my reader *did* sync by writing files to iDisk. It didn’t work very well at all, and, looking back, I shouldn’t have shipped this feature. I made a mistake.

Syncing for RSS readers seems like it should be easy. In the simple case, you have three things to sync:

1. The list of feeds (probably as an <a href="http://www.opml.org/">OPML</a> file).

2. The list of articles that have been read.

3. The list of articles that have been flagged.

It seems like all you have to do is make each copy of your RSS reader read and write three files to Dropbox, one file for each item in the list above.

It seems like each reader could just read the files at startup and write out new files when it quits. Problem solved!

But not even close.

#### Apps run for a long time and run at the same time

If you launch a reader on your Mac and on your iPhone, it’s entirely likely that you might leave it running for days or weeks. That means that the apps would have to read and write periodically.

That leads to a couple questions:

* How often should they check those files for changes? The more they check, the more performance is hurt. But the less they check, the less in-sync the apps are.

* What happens if two or more apps want to access the same file at the same time?

* What if you add a feed on one reader and delete a feed on another? If each app writes the entire feeds list, then one reader will see that the added feed isn’t in the list. Was it deleted? There are other easily-imaginable conflicts. You don’t want to constantly harass the user by asking them questions.

#### Lists can get very big

If you could solve the problems above, a large feeds list wouldn’t be too big to read periodically.

On the other hand, the list of read articles could be massive. It would get bigger every day. Reading and writing this entire list, were it a single file, would become a giant performance problem.

It would also be very prone to conflicts: if something isn’t on the list, but one reader thinks that item was read, does that mean the user marked it as unread, or does it mean that the other reader just hadn’t seen that item yet, or...?

If you could solve the conflicts problem, you could mitigate the size and performance issue by saying that you’ll only sync read states for recent items, for the last two weeks or a month.

Note that Google Reader syncs read states for just recent items, though the rules are a bit more complex than just n days. Doing it in a similar way would be a support issue forever, since people would still expect *everything* to be synced without any performance penalty — and rightly so.

#### Flagged articles may no longer appear in subscribed-to feeds

What happens if you flag an article, and then that item drops off the feed it’s in? Or what if you flag an article but then delete that feed later?

I think you expect to keep that article forever, or until it’s unflagged.

That means that you’d have to store the entire contents of the flagged articles on Dropbox too. For some people that could grow to a sizeable amount of data. Maybe not for most people, but the system has to be built to accommodate all users.

And, again, you have the issue of conflicts — and the consequences of losing a flagged article could be very bad.

#### Lists will not work

The above almost makes it sound like lists could work: all you’d need are policies to keep the sizes down, methods to deal with multiple apps wanting to read and write at the same time, and systems to deal with conflicts.

You could do the first two, but there are certain types of conflicts you can’t handle with this approach (particularly regarding deleting things).

In other words, the “just store the app data on Dropbox” approach won’t work.

#### A system that would work

I’ve worked with four different RSS syncing systems, and every one of them had holes. The ideal syncing system would work something like this:

An RSS reader would report actions and times to the system. For instance, it would tell the system things like this: "[Feed] was added to [folder] at [datetime]" and "[Feed] was deleted at [datetime]" and "[ArticleID] was marked unread at [datetime]."

By making deletes explicit and by including dates and times, the system would be able to deal with the conflicts that the list-of-data approach couldn’t handle. (A last-action-wins policy is sensible here.)

However, when pulling data, the clients would not want a replay of the actions: an RSS reader would want the current state of the feeds list, and lists of articles marked read/unread and flagged/unflagged since the last pull request. In other words, the system would have to have some smarts — it would have to know how to put that data together. Plain old files don’t have that kind of smarts.

(Why not just replay the actions? Say you just added a reader on your iPhone and you didn’t have one before, but you’ve been syncing for a year. Should the app on your iPhone download a year’s worth of actions? No.)

This system needs a web app with a database. The web app would not have to have an HTML UI: it could be built solely to support syncing, and be otherwise invisible.

But a web app with a database isn’t free — someone has to write and maintain the code and someone has to run it. Developer hours cost money. Bandwidth, storage, and CPU time cost money.

(And no, you can’t just put a SQLite file on Dropbox and use that for this case. Remember that each client would see a copy of the database — Dropbox just treats it like any other file that should re-sync on change.)

#### Mind the gap

The system described above would keep feeds and article states consistent between multiple readers, and that would be all that I personally would require. But it wouldn’t be enough for everybody.

The system above doesn’t handle this scenario:

Say you like to keep the last two weeks of articles in your readers. You normally read on your Mac, and you haven’t launched the reader on your iPad in a week. When you do, you expect your iPad to have the exact same articles that your Mac has.

But it doesn’t — it’s missing some, because some articles have fallen off the feed. So you write to support and explain that syncing isn’t working for you, because there’s a gap in the articles on your iPad. You prove it easily with screen shots comparing the same feed on your Mac and on your iPad.

To handle this case, the syncing system needs a feed retrieval system that would read and store the contents of all the feeds known by the system once an hour or so.

What happens when there are a million feeds in the system? This gets expensive. I wouldn’t be surprised if the feed retrieval part of this becomes the most expensive part by far.

#### And in the real world

Nobody wants to build and run this because there’s no money in it.
