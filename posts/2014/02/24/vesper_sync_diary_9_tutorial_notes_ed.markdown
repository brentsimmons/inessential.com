@title Vesper Sync Diary #9 - Tutorial Notes Edge Case
@pubDate 2014-02-24 17:23:51 -0800
@modDate 2014-02-24 22:06:59 -0800
A question that’s been bugging me for a while is what to do about the tutorial notes that you get when you first launch Vesper.

#### The Problem

Launch Vesper on your day phone. The tutorial notes are created with some random IDs.

Launch Vesper on your night phone. Tutorial notes are created there too, with some other random IDs.

Now turn on syncing on both phones. What happens?

You get multiple copies of the tutorial notes on both phones, since, technically, they’re separate notes.

#### Original sync architecture

Even though 1.0 didn’t have syncing, it was built with syncing in mind. One of the early decisions was that each note would have a UUID that would be unique across the entire system.

So every time the app generated a tutorial note, it would generate a new UUID. Which meant that the same tutorial note on different devices was really two different notes.

#### Updated sync architecture

Along the way toward actually implementing syncing I made a change to how notes are identified. Each note has a 64-bit integer ID, and it’s unique only for a given account.

#### Back to the problem of tutorial notes

As I was thinking about this problem again today, I realized that it’s now safe to use predefined IDs for notes.

I could always give the first tutorial note an ID of 1, for instance — because it’s totally fine that the IDs aren’t unique to the system.

(I revised the note ID generator so that it reserves 0 - 1000 for app use.)

#### But how do we do this retroactively?

What about people who are already using Vesper and already have the tutorial notes — and they already have note IDs?

We have data migration code mandated by the switch from FMDB/SQLite to Core Data. While migrating, that code checks a note to see if it’s a tutorial note, then, if it is, assigns it the correct predefined ID.

(All note IDs are reassigned anyway since we’re going from UUIDs to 64-bit integers.)

There’s just one remaining edge case. The problem comes with detecting that an existing note is a tutorial note. The tag has to be the “Tutorial” tag *and* the text has to match exactly. If a tutorial note has been edited, it won’t be detected as a tutorial note.

Which means that you could end up with that edited version plus a new version of that note from another device.

This is just going to have to be fine. It’s not ideal, but I can’t think of a way to handle it. (I wish that I had marked tutorial notes as such in the v1 database, but I didn’t. I am now, though.)
