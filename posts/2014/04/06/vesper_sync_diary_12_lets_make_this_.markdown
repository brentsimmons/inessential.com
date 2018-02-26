@title Vesper Sync Diary #12 - Let’s Make This Change No Matter How Late
@pubDate 2014-04-06 15:37:44 -0700
@modDate 2014-04-06 15:37:44 -0700
For a couple hours yesterday I was convinced I was going to change how user account info is stored — I was going to switch from SQL to table storage. ([Azure table storage](http://azure.microsoft.com/en-us/documentation/articles/storage-nodejs-how-to-use-table-storage/), a variety of NoSQL.)

Reason: I don’t know how the data model for accounts will change. I’m sure we’ll add to it, but I can’t guess what we’ll need. At the moment it’s nothing more than username and the little needed to make authentication work.

It’s not that I suspect we’ll want to store more personal information. It’s likely we’ll never even store your *name*, even. There’s nothing in it for us — storing things like that would just make the database larger for no good reason.

But you could imagine there might be some preferences and settings that should get synced. I just don’t know what they will be.

Table storage is a *great* answer for that because it’s schema-less. A single row can have an arbitrary collection of key/value pairs. (Subject to some data size limits.) Sounds perfect.

#### But it’s too late! Don’t do it!

Making this change would delay shipping. And it’s really, really hard to justify any delays.

But here’s the thing about web services: it’s way easier to change things before shipping than after. Once the app ships, any changes to the backend have to be made with extreme care.

And a change as large as switching account info from SQL to table storage means stopping the world, migrating the data, then restarting the world. (And testing beforehand. And after. And rehearsing. Multiple times.)

That’s not something I ever want to do. It may be inevitable some day, but I sure hope to avoid it.

So that’s how I justified making the change. A little pain now saves bigger pain later.

#### But then I didn’t do it anyway

As I started mapping out the implementation, I ran into a snag.

I want user IDs to be a 64-bit integer, because those user IDs are stored in the notes, deletedNotes, and tags SQL tables. SQL provides an auto-incrementing row ID which is perfect.

If I used the actual username as user ID instead, the databases would be much larger. For performance reasons we want to keep the database as small as possible. (For cost reasons too — but our attitude is that better performance pays for itself. Luckily the two values are aligned in this case.)

So I thought some more about the future. What I’m really worried about is *adding* to the data model, and that’s actually not that hard. We could add SQL columns and tables to store the additional data — or even use NoSQL table storage to add associated data. (Whatever is the smartest move.)

This is not nearly as bad as doing a full migration of data from one type of storage to another. If I had thought it through initially I wouldn’t have looked at NoSQL table storage at all.

But I’m glad I did, because I’ve learned some things about my environment, and that’s always a good thing.
