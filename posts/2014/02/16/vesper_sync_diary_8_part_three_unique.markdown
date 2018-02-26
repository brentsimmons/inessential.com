@title Vesper Sync Diary #8 part three - Unique IDs and Hashing
@pubDate 2014-02-16 22:05:59 -0800
@modDate 2014-02-16 22:05:59 -0800
In <a href="http://inessential.com/2014/02/16/vesper_sync_diary_8_part_two_more_abo">More about Unique IDs</a> I decided to use a client-generated UUID for notes.

<a href="https://twitter.com/brentsimmons/status/434132669975130113">But I’ve been thinking</a> that there’s an alternative where I could use a 64-bit integer instead of a (128-bit) UUID: <a href="https://code.google.com/p/cityhash/">CityHash</a>.

The thing about 64-bit values is that they’re much easier to handle than 128-bit values. For example, the Core Data modeler has Integer 16, Integer 32, and Integer 64, but no Integer 128.

So the idea is this: when I need a 64-bit ID, I create a new UUID and then pass it to CityHash64().

There is no practical reason to worry about collisions — especially given that an ID has to be unique per-account, not system-wide.

Nevertheless, a test to put my mind at ease would be a good idea. I’ll write a little app that generates a few million of these from UUIDs and make sure I don’t see collisions.
