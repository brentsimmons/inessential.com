@title Vesper Sync Diary #11 - Scaling
@pubDate 2014-03-25 18:05:45 -0700
@modDate 2014-03-25 18:05:45 -0700
I have no idea what’s going to happen the day we ship Vesper with syncing. I don’t know what traffic will be like.

My job is to make sure our servers can handle it, no matter what — which means I’ve thought a lot about scaling.

#### The Big Thing

The heart of the app is notes and tags, and it’s tempting to start by thinking about the notes and tags database and the API server.

But that’s not really the big thing. The big thing is *pictures*.

One single picture may be bigger than a given user’s notes and tags. A user with several pictures will almost always have more in picture data than in notes and tags.

We’re solving that problem like this:

* Pictures are stored in Amazon S3. They’re not stored in a folder on our server; they’re most definitely not stored in a SQL database.

* Client apps talk directly to S3. Pictures are not uploaded to our API server and then sent to S3 — the picture data never hits our API server. (The API server does, however, build connection strings for clients to talk to S3. But that’s super-fast and not a burden on the API server.)

I have no doubts about S3’s ability to scale. It handles much larger systems than ours.

And because the API server doesn’t have to handle binary uploads, it’s free to handle notes and tags syncing.

#### Notes and Tags Syncing - Deltas

The worst thing I could is upload the entire database and download the entire database. The trick is to do deltas — upload only the things that have changed, and download only the things that changed on the server.

Each note has a serverModificationDate field on the server. When a note changes on the server, that field is updated to the current time. It’s *not* a client-modified date — it has to be the date modified on the server.

When a client asks for notes with recent changes, it sends an <a href="http://inessential.com/2013/11/12/vesper_sync_diary_5_sync_tokens_and_e">opaque sync token</a>  that the server decodes to a date. That date ends up in a SQL query on the serverModificationDate field.

Note, though, that I return an entire note when it’s been changed. I could return only the changed fields, but that would mean keeping a server-modified-date for each field, which means more code and a bigger database. I think it’s worth sticking with one field and returning an entire note.

#### Data simplification

In Vesper 1.0 notes were identified by a UUID string — which is a string 36 characters long. For a client-only database that’s not the worse thing ever.

But when you have a server with <em>everyone’s</em> data (everyone who syncs) then it’s important to try to reduce database size. So I switched to using a 64-bit integer as the primary key for notes.

It’s a small bandwidth saving, but it’s a big saving in database size.

(Last time I wrote about this I was <a href="http://inessential.com/2014/02/16/vesper_sync_diary_8_part_three_unique">considering using CityHash</a>. But just using SecRandomCopyBytes and checking for collisions is simpler. Since, on the server, the primary key is note ID + user ID, I don’t have to worry about collisions across users.)

Another simplification: I’m not syncing properties that could be calculated.

Some of the obvious ones are things like the links property. Though it’s stored in the database on the client, there’s no need for the server to know about this. The client can regenerate the links array for a note whenever its text changes.

(Other client-only database fields: links, thumbnailID, truncatedText.)

#### Handling Deleted Notes

The easy way to handle a deleted note is a `deleted` column in the notes table. But this isn’t the best use of space.

Instead there’s a deletedNotes table that stores only note IDs. (On both client and server.)

This means that when a note is deleted it’s gone from the server — its row in the notes table is deleted, and its ID is added to the deletedNotes table.

#### Cheating

The client database in Vesper 2.0 has four main tables: notes, tags, attachments, and deletedNotes. It has two lookup tables that relate ordered tags and ordered attachments.

The server database has just three main tables: notes, tags, and deletedNotes. And it has *zero* lookup tables.

Though a note can have many attachments, a given attachment relates to just one note. Were attachments a separate table, retrieving notes would also mean fetching from the attachments table. But instead I’m storing the attachments as JSON in an attachments column in the notes table.

I’m doing something similar with tags: the tag names for a note are stored as JSON in a tags column in the notes table.

You might argue that this is the wrong way to do it, and I’d understand that argument and generally agree. (And, in fact, the client database is structured the way you’d recommend.)

But by doing things on the server this way I get a couple benefits.

* Much simpler code on the server.

* Easy and fast fetches. The server can retrieve a note with one call to one table and no joins — the fastest-possible fetch. It doesn’t *also* have to fetch from two lookup tables and from tags and attachments tables just to retrieve a note and its relationships.

#### Node

This is all running in Node.js on a system where I can easily increase the number of instances as needed. Node is reputed to be fast at things like this.

#### Summary

Pictures are handled by S3, which scales.

The API server itself shouldn’t be a bottleneck.

The only bottleneck is the database, since there’s just the one. I’ve done everything I can think of to keep it small and simple. The server is fetching just changed objects, and the queries are all kindergarten SQL with no joins. The appropriate indexes have been created.

So — in theory — scaling on day one will just be a matter of making sure there are enough instances of the API server running. How hard could that be?

PS I think I wrote this mainly to reassure myself that it’ll be okay.
