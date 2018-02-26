@title Vesper Sync Diary Follow-up
@pubDate 2014-05-24 12:05:16 -0700
@modDate 2014-05-24 12:05:16 -0700
This is probably the last of the Vesper Sync Diary posts — there’s not much left to write about the design. But I should go back and note which things I wrote about are no longer true, and why. I’ll go article-by-article.

#### [Vesper Sync Diary #1 - Syncing Tags](http://inessential.com/2013/10/01/vesper_sync_diary_1)

I especially like this article because it introduced the day-phone/night-phone thing as a way to talk about syncing. Please feel free to use that yourself, if you like.

This article describes tags syncing exactly. No changes.

#### [Vesper Sync Diary #2 - Core Data](http://inessential.com/2013/10/05/vesper_sync_diary_2_core_data)

I didn’t end up using Core Data.

#### [Vesper Sync Diary #3 - Immutability, Deleting, and Calculated Properties](http://inessential.com/2013/11/05/vesper_sync_diary_3_immutability_del) 

This article is accurate except for a few details. The main one is that we don’t have a DeletedObjects table — we have a DeletedNotes table. The schema on the server for deletednotes:

<code>id bigint, userID bigint, noteID bigint, serverModificationDate datetimeoffset(3)</code>

On the client:

<code>uniqueID integer</code>

#### [Vesper Sync Diary #4 - In Another Country](http://inessential.com/2013/11/07/vesper_sync_diary_4_in_another_countr)

I didn’t write about my biggest frustrations with JavaScript. That deserves its own post.

#### [Vesper Sync Diary #5 - Sync Tokens and Efficiency](http://inessential.com/2013/11/12/vesper_sync_diary_5_sync_tokens_and_e)

Accurate.

#### [Vesper Sync Diary #6 - Merging Notes](http://inessential.com/2013/11/13/vesper_sync_diary_6_merging_notes)

Accurate.

#### [Vesper Sync Diary #7 - Audibles](http://inessential.com/2014/01/02/vesper_sync_diary_7_audibles)

Partly accurate.

On the server, attachment metadata is stored in a column in the notes table. Stored as a JSON string.

On the client, attachment metadata is stored in a separate table, called attachments:

<code>uniqueID TEXT UNIQUE NOT NULL PRIMARY KEY, mimeType TEXT NOT NULL, height INTEGER, width INTEGER</code>

#### [Vesper Sync Diary #8 - The Problem of Unique IDs](http://inessential.com/2014/02/15/vesper_sync_diary_8_the_problem_of_un)

This article had many follow-up articles:

[Vesper Sync Diary #8 part two - More about Unique IDs](http://inessential.com/2014/02/16/vesper_sync_diary_8_part_two_more_abo)<br />
[Vesper Sync Diary #8 part three - Unique IDs and Hashing](http://inessential.com/2014/02/16/vesper_sync_diary_8_part_three_unique)<br />
[Vesper Sync Diary #8 part four - Random IDs](http://inessential.com/2014/02/17/vesper_sync_diary_8_part_four_random_)<br />
[Vesper Sync Diary #13: Unlucky Numbers](http://inessential.com/2014/04/13/vesper_sync_diary_13_unlucky_13)<br />
[Vesper Sync Diary #13 part 2 - Maybe It’ll Be UUIDs After All](http://inessential.com/2014/04/14/vesper_sync_diary_13_part_2_maybe_it)<br/ >

In the end: unique IDs for notes are random 53-bit positive integers. The client checks for collisions. (A note ID only needs to be unique for a given user, so this works out.)

The notes table on the server has a primary key that’s a monotically increasing bigint. It has a constraint that each noteID/userID pair has to be unique.

#### [Vesper Sync Diary #9 - Tutorial Notes Edge Case](http://inessential.com/2014/02/24/vesper_sync_diary_9_tutorial_notes_ed)

Accurate.

#### [Vesper Sync Diary #10 - Data Migration](http://inessential.com/2014/02/24/vesper_sync_diary_10_data_migration)

This article references Core Data, but we’re using [FMDB](https://github.com/ccgus/fmdb) + SQLite. (I write the model layer of my dreams. If I had plans for other apps, I could use it. It’s exactly what I want.)

Instead of storing a boolean that says whether or not migration happened, I do this instead:

If the v1 database exists, run the migration. On completion, rename the v1 database. (Don’t delete it.) That’s it.

#### [Vesper Sync Diary #11 - Scaling](http://inessential.com/2014/03/25/vesper_sync_diary_11_scaling)

This is more about performance than scaling.

(In [Scaling and Performance](http://inessential.com/2014/04/18/scaling_and_performance) I talk about scaling.)

The article mentions Amazon S3 — but we ended up using Azure blob storage instead. (Which is very similar.)

Otherwise the article is accurate.

#### [Vesper Sync Diary #12 - Let’s Make This Change No Matter How Late](http://inessential.com/2014/04/06/vesper_sync_diary_12_lets_make_this_)

In this article I considered switching from SQL to table storage for account data. Table storage is *much* cheaper, and everybody likes NoSQL these days.

I did not make that switch. I stuck with SQL — for the reasons the article talks about, but also because all my experience in the last ten years or so has been with SQL, and it’s worth sticking with something I understand well.

#### [Vesper Sync Diary #14 - Keys](http://inessential.com/2014/04/17/vesper_sync_diary_14_keys)

Accurate.

#### [Vesper Sync Diary #15 - Server Testing](http://inessential.com/2014/04/19/vesper_sync_diary_15_server_testing)

I’m still writing tests.

#### [Vesper Sync Diary #16 - Debugging Syncing](http://inessential.com/2014/05/13/vesper_sync_diary_16_debugging_syncin)

I haven’t had to do much debugging — but it sure is nice to control all parts of the system.

It does make for craziness where I have Xcode open with the client app, BBEdit open with the API server, several Terminal tabs open, and several Safari tabs opens (server log, for instance). And the app running in the simulator *and* the app running on my iPhone.

It may be a distributed system, but I can see and affect all the parts on my computer. Sure beats getting frustrated with someone else’s server bugs.
