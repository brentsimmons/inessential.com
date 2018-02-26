@title Vesper Open Source #2: the API Server
@pubDate 2016-12-19 14:14:19 -0800
@modDate 2016-12-19 14:16:23 -0800
I just posted <a href="https://github.com/brentsimmons/vesper-api">Vesper’s API server</a> up on GitHub.

Again: this is provided as historical artifact, not as living software. It no longer runs anywhere. And I don’t make claims about quality — it’s just that it may be interesting. (And may not be.) It gives me something to write about, at least.

For possibly-helpful background, see the <a href="http://inessential.com/vespersyncdiary">Vesper Sync Diary</a>, which was written while I was working on this code.

#### Azure Mobile Services

It’s a Node.js server — but it ran on top of Mobile Services, which means you couldn’t just plop it down on a machine and run it unless you added the exact features that Mobile Services provides.

Nevertheless, I think the code is somewhat readable, even if it would be difficult to run it. (You’d also have to set up a database with the exact same schema, which you could figure out from the code. I don’t recommend actually trying to get this running.)

#### Where the code is

See the api and shared directories. You can ignore the extensions and table directories. The scheduler directory has just one simple script in it.

#### Things I Liked

The Azure folks provided a _ton_ of help. They were great, and I enjoyed using the service.

Once the code was written and tested, I made almost no changes. It just worked. And keeping it running wasn’t a problem until near the end (I think I had to upgrade the database plan, and that fixed it).

#### Things I Didn’t Like

It’s JavaScript. Because I’ve spent the last 15 years writing Objective-C, I would have been far more comfortable writing in Ruby. It would have been more readable and better-organized. Hopefully I could have better avoided callback-hell (where callbacks are nested inside callbacks which are nested inside callbacks, etc.).

But, hey, JavaScript gets the job done.

The other thing I didn’t like was that there wasn’t a way to run a Mobile Services Node site locally, since the online version takes care of a bunch of things. In practice this wasn’t as bad as it sounds, but being able to run it locally would have been nice.

#### The Heart of Vesper Syncing

See api/notes.js. Syncing was done per-property: each property of a note had an associated modification date. When notes come into the server, and there are existing versions, those properties are merged. See the `mergeOneNote` and `mergeOneProperty` functions.

It should be no surprise that almost the exact same code — only in Objective-C — runs on the client side. It also merges property-by-property as notes come from the server, since there may be local changes that are newer.

Also see, in api/tags.js, `mergeTags` and `mergeTag`.

#### Encryption

The text of notes was stored in the database encrypted, with a key that was stored in the config for the site but not in the source code or in the repository. In shared/vespernotes.js, see `encryptedTextForNote` and `decryptedNoteText`.

One of the features of this was that I could change the encryption key without re-encrypting the entire database. The keys were stored with names of the form `VESPER_TEXT_KEY_0`, `VESPER_TEXT_KEY_1`, etc. And there was another config item that specified the current key. When the current key failed to decrypt note text, it would try the previous key, and so on back to the very first (zeroth) key. See the loop in `decryptedNoteText`.

This is different from providing end-to-end encryption, of course. These days that’s probably the way to go. But at the time we wrote this it was reasonable not to do that. Times change.

(Note that nobody ever asked for any data from our system, and we would have to create a mechanism for that, which we never did.)

