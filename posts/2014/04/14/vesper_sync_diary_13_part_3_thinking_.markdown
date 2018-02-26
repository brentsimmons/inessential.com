@title Vesper Sync Diary #13 part 3 - Thinking Too Much
@pubDate 2014-04-14 17:56:31 -0700
@modDate 2014-04-14 20:53:41 -0700
There are two pieces of advice I’ve been getting:

One is that I’m [thinking too much](http://inessential.com/2014/04/14/vesper_sync_diary_13_part_2_maybe_it) about this. It’ll be fine if I have a properly normalized schema and I use the appropriate indexes. After that, don’t worry.

(I admit that I’m prone to going down every performance rabbit-hole I can find.)

The other — partly related — is that the right way to deal with the notes table is to do create a clustered primary key as userID + noteID. This way all notes by a given user will be together.

And this is the default behavior. It’s good. Smarter people than I am have thought about this.

And I can drop the integer identity column.

<i>Update a few hours later:</i> No. Wait. The [best database guy I know](https://twitter.com/GlennAlanBerry) tells me to do it the way I was thinking: surrogate key integer identity column as clustering key.

He also suggests I don’t need to add a unique constraint for noteID + userID, since noteID is a UUID. A unique constraint on noteID is all that’s needed.
