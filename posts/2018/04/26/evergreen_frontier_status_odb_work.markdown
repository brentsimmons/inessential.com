@title Evergreen/Frontier Status: ODB Work
@pubDate 2018-04-26 13:20:10 -0700
@modDate 2018-04-26 13:22:04 -0700
For the past few days I’ve been working on adding [Frontier-like object database](http://scripting.com/2018/04/18/164609.html) (ODB) support to my [database framework](https://github.com/brentsimmons/RSDatabase/tree/master/RSDatabase/ODB).

It’s not finished yet — it doesn’t even build.

#### What it is (or, what it will be)

It’s hierarchical key-value storage. No schemas. Tables can contain tables, with no limit.

This implementation is the lowest level: the part that gets, sets, and deletes data from the database.

It’s application-agnostic, at this level — it doesn’t know about all of Frontier’s data types, for instance. A level on top of this will be needed for [new-Frontier](https://github.com/brentsimmons/Frontier).

#### SQLite, my favorite hammer

I’m not actually writing a new database — I’m using SQLite. And that’s because I’ve been using SQLite for 15 years, and I love it and know it well, and I know how incredibly stable it is. I’m not willing to write my own thing, and I’m not willing to use a thing less mature and rock-solid than SQLite.

How it works:

The [schema](https://github.com/brentsimmons/RSDatabase/blob/master/RSDatabase/ODB/ODB.swift) is pretty simple. There are tables and values.

Every table has an `id`. Every table (except the root table) has a `parent_id` that points to its parent table.

And every value has an `odb_table_id` that points to its parent table.

This way it’s easy to get a table’s children: it takes just two `select` statements.

(Both tables and values also have a `name`, since this is key-value storage.)

Tables and values will be cached in memory, so not every call will require a database read.

(Before you suggest I use something other than SQLite, know that I won’t change my mind on this.)

(Also, again: it’s not done yet. Doesn’t even build.)

#### Why I’m doing this now instead of something else

I’m using schema-less storage for feeds in Evergreen. (Articles and article status, on the other hand, are stored using a schema, in SQLite.)

Currently I’m writing a big binary plist with all the feed data, and it has to be rewritten every time a feed property changes. The writes are coalesced — but still, this isn’t great.

I’m using schema-less storage in part because of syncing systems: I don’t know, and can’t guess, what I’ll need to store. Different systems will have different requirements.

Also: I may add features later that require additional feed properties. I don’t know what those are.

I realized that what I really want for this is a feature from Frontier: hierarchical key-value storage.

Each system will gets its own database on the client. For each, I’ll create an odb table called `feeds`. Each feed will have its own subtable. The key will be its id (which may or may not be its URL, depending on the syncing system).

And inside each subtable I can put whatever I want, at any time, without having to change any schemas or implementations.

Example:

For the On My Mac account — not synced; reads feeds directly — we keep track of Etag headers in order to support conditional GET. So, for example, I’d want to get, set, and delete `feeds.[feedID].etag.ifModifiedSince`.

But with most syncing systems we get the feed content from the system itself — not by directly reading the feed. There might be some other data from the service to store: `feeds.[feedID].syncToken`, for instance.
