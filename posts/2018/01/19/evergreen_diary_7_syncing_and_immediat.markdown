@title Evergreen Diary #7: Syncing and Immediate and Deferrable Actions
@pubDate 2018-01-19 13:29:16 -0800
@modDate 2018-01-19 13:29:16 -0800
There are, as I [mentioned previously](http://inessential.com/2018/01/17/evergreen_diary_6_proposed_sync_design), two types of syncable actions: immediate and deferrable.

An *immediate* action is something like adding a feed: it requires that the server is reachable right now, so that the feed actually gets added.

A *deferrable* action is something like marking articles as read. The sooner the server knows, the better, sure — but it can wait if necessary. It can even wait for weeks or months.

I’ve decided to make it simple and categorize these actions like this: any structural action that affects the list of feeds and folders (or tags) is an immediate action, while any action that affects the status (read, starred) of articles is deferrable.

Or, in UI terms: if it’s something you do in the sidebar, it’s immediate; it it’s something you do in the timeline, it’s deferrable.

Most importantly: you can read articles while you’re offline.

#### Discarded alternate approach

You could argue that *all* actions should be deferrable. For instance, Evergreen could remember that you want to add a given feed, and add that add-feed action to the sync queue and wait for the server to become reachable again.

But doing so would add more chance for conflicts. Consider the case where the add-feed action got queued (on your day Mac) and then just sat there. Then, on your night Mac, you add the feed and it succeeds — then you decide you don’t like it after all, then delete it.

The next day, back on your day Mac, the add-feed call finally goes through, and then you have to delete it again. (And then you report an Evergreen syncing bug.)

There are other issues as well: do you add the feed locally? And read it? No, because this gets ambiguous quickly, as Evergreen’s article IDs won’t match the article IDs the server has assigned. Evergreen might not even have found the same feed URL the server found (in the case where you just gave it a website URL).

So we’ll stick with these two categories, immediate and deferrable.

To refine the definitions: a deferrable action is one where the state change can be reflected locally without risking serious conflicts or ambiguity.

#### Immediate actions

These will result in an immediate API call, and the result will be reflected in the UI. This is straightforward.

#### Deferrable actions

These actions will be stored in a database.

The simplest way to do this is probably a set of tables: articlesToMarkRead, articlesToMarkUnread, articlesToStar, articlesToUnstar. Each table would have one single column: `articleID`.

This layout is probably the most efficient way to add/delete articles.

This is not actually an ordered queue, but I think that’s okay. Most of the time all four tables will be empty.

When articles are marked read (for instance), then those articles will be added to articlesToMarkRead and deleted from articlesToMarkUnread. The system will then know that it has pending status changes to the send to the server.

Then, periodically, the app will attempt to contact the server. Most of the time this should happen within a minute or so.

Part of the idea is using this system to coalesce calls: the app shouldn’t call the server every time you select an article (which marks it read). Better to update the database and call the server very-soon-ish, but not necessarily this exact second, to allow for multiple articles to queue up.

The downside to this particular layout, which may make me change it, is that supporting additional status types means adding more tables. But the alternative is to add more columns to a single table, which is better but not necessarily that much better.

Another downside is that there’s no automatic guarantee that an article ID won’t exist in, say, both articlesToMarkRead and articlesToMarkUnread at the same time. But the answer here is simple, careful coding: a single bottleneck function that never adds to one without deleting from the other.
