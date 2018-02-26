@title Vesper Sync Diary #8 - The Problem of Unique IDs
@pubDate 2014-02-15 22:21:46 -0800
@modDate 2014-02-15 22:25:00 -0800
In an RSS reader there are a couple ways of setting unique IDs.

If the sync server also fetches the feeds — if it’s a content service — then the sync server can arbitrarily assign unique IDs. (An auto-incrementing 64-bit integer would suffice.)

(Yes, it has to be 64 bits, not 32. I remember when NewsGator’s content server broke the 32-bit max barrier. Some of the client apps weren’t expecting this and had to be revised quickly. Luckily NetNewsWire was prepared for this, but it was more-or-less by chance.)

A second way is to have the sync server and all client apps agree on an algorithm for generating unique IDs. It might be feedURL plus guid (if present, permalink if not, etc.)

But Vesper is a note-taking app, where the content is generated on the device. And a note doesn’t have any relatively stable properties you can use to create an ID (while an RSS item’s guid or permalink usually doesn’t change).

How should it generate unique IDs?

#### Generating IDs on the client

If a client app generates a unique ID, it can’t use an auto-incrementing 64-bit integer, since there’s no good way to coordinate these between clients and the server. You’d get collisions for sure.

A client app could instead generate a UUID when creating a note and send that to the server with the note.

There are some drawbacks to that:

1. A UUID is a 128-bit number. It sures seems like 64 bits ought to be enough for any unique ID, but this is double the size. The database will be larger than it needs to be.

2. A bad client could send a bad UUID. It could do this on purpose, in hopes to disrupt the integrity of the data or to gain access to data it shouldn’t get.

3. UUIDs could collide, and the result could be someone getting someone else’s data.

I’ll dispense with these. Mostly.

The size issue (#1) isn’t that bad. A 64-bit unique ID would be best, but using 128 bits instead shouldn’t have a significant impact on performance or costs.

The issue of bad clients (#2) and collisions (#3) can be mitigated by making it so that a unique ID is considered unique only for a given user. (Not that there ever was a practical chance of UUID collisions. The chance of a bad client is higher.) (In the database I’d make the primary key a compound key of uniqueID and userID.)

A bad client would thus be able to trash an individual user’s data but wouldn’t be able to affect the rest of the data.

(I have to design as if terrible things could happen — because by doing so I can better prevent terrible things from happening.)

#### Generating IDs on the server

You’re nodding your head. “Brent! Yes! This is the way to go! Don’t trust the client!”

I hear you.

The server could generate an auto-incrementing 64-but unique ID. And I wouldn’t have to do compound primary keys, since I could trust the unique ID.

Were I doing a web app I’d certainly make it work this way.

But since it’s a mobile app, everything is asynchronous. Sending a note to the server and getting back a unique ID happens some time after it’s created. (Could be a fraction of a second; could be hours, days, or weeks.)

To make matters worse: a note might get edited as it’s in flight to the server.

It seems like the way to make this work is to give a note a temporary client-specific unique ID. When sending the note to the server to get its canonical unique ID, the client would expect the server to return that temporary ID along with canonical ID. (That way I could match up the local note with its canonical ID.)

That’s do-able. That’s just housekeeping code. Not grave.

#### Here’s the scenario that stops me

Say you sign out. All the canonical unique IDs stored locally are deleted — because, after all, they’re no longer valid, since you might sign back in with a different account.

Then you sign back in. Maybe it’s the same account and maybe it’s a different one. How does the client know which notes are already stored in the server for that account and which ones aren’t?

Consider this: the client then sends a note to the server that the server already has, but the client didn’t send the server’s unique ID, because it deleted that information.

Should the server treat it as a new note? Or should it look to see if there’s an exact duplicate? (That’s a crazy amount of work the server would have to do every time it received a note without a server ID.)

It might not find an exact duplicate because the note has been edited. So now it’s two separate notes when it should be just one.

#### Storing different unique IDs per account

One solution — that I don’t like — is that the client could store multiple unique IDs per note, a different unique ID for each account.

This way it wouldn’t have to delete unique IDs on signing out. When talking to the server it would reference the correct ID based on the signed-in account.

When I imagine implementing this I just don’t like it. (I’m going to stuff a dictionary in a uniqueID property? Ugh.)

#### Combination approach

The client could generate a unique ID *and* the server could generate a unique ID.

Almost all of the time the server’s unique ID would be thing actually used. The client ID would be a backup ID to be used in the case when a note *may* exist on the server but the client doesn’t know that. (Because you’ve signed out and then signed in.)

On receiving a note without a server ID, the server would check see if a note with that client ID exists for that account. If so, then it would return the server ID for that note. If there is *no* note with that client ID for that account, then it’s a new note and it generates a new server ID.

That client ID would have to be a UUID, while the server ID would be a 64-bit integer.

I don’t love this approach, because it seems a little weird to have to give everything *two* IDs. I’ve now talked myself into 192 bits for each row on the server to store unique IDs. 

The code is less weird than the unique-ID-as-dictionary approach. So I think that’s how I’ll do it.

But if you have a better idea, you can find <a href="https://twitter.com/brentsimmons">me on Twitter</a>.

P.S. It occurs to me later that a client ID could just be its creationDate timestamp. With millisecond precision. Since the client ID only has to be unique for a given person (across one person’s accounts) that might be okay. And since I’m already storing creationDate, that means I wouldn’t have to generate and store a UUID. Would any single person run into timestamp collisions? It’s hard to imagine.
