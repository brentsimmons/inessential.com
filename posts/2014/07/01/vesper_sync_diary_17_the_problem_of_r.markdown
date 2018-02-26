@title Vesper Sync Diary #17 - The Problem of Relationships
@pubDate 2014-07-01 09:48:26 -0700
@modDate 2014-07-01 10:01:30 -0700
While I was talking with some folks yesterday about syncing-in-general, the issue of relationships and incomplete object graphs came up, and I realized I hadn’t written about it.

Here’s the problem: an object with relationships to other objects may have been synced — but those related objects haven’t been synced yet.

In other words, in Vesper terms, a note may have been synced, but its tags and attachment metadata haven’t been synced yet. How do you deal with this?

Answer: you design the system so that this doesn’t happen.

In general this means that when an object is sent to the server, and when an object is returned from the server, its related objects are also included.

In Vesper’s case, when it sends notes to the server it also includes attachment metadata and the names of its tags (in order).

Even though local storage has three separate tables (notes, tags, attachment metadata), there’s nothing that says we can’t add related objects to the JSON version of a note.

Attachment metadata objects are included in their entirety (uniqueID, mimeType, height, width), but we cheat a little bit with tags: we include their names only. But since a tag’s unique ID is the lower-case version of its name, a client can create a tag object with just its name.

I’ve considered a different (but similar) solution. Instead of separate calls for syncing tags and notes, there could be just one call. The client would send two arrays in that one call: one array of changed tags, one of changed notes. The response from the server would be in the same format, and the tags array would include every changed tag and every tag related to a note in the notes array.

But the current system is working well, and the only real reason to change is to cut down the number of API calls. (Number of API calls isn’t a problem for us, either on client or server — Vesper syncing is already fast and efficient. But I don’t mind improving on things that are already good.)
