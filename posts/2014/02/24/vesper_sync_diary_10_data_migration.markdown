@title Vesper Sync Diary #10 - Data Migration
@pubDate 2014-02-24 18:55:15 -0800
@modDate 2014-02-24 20:54:15 -0800
This is the not-fun part. Not only has the data model changed, we’ve moved from FMDB/SQLite to Core Data. There’s no way out of doing data migration.

As with syncing, any bugs here are potential data-loss bugs. This code demands the utmost care.

Assume tests. Assume that the code is written to handle unexpected conditions so that it won’t trigger an exception. Assume careful memory use.

The biggest concern is crashing in the middle of the migration. While I believe the migration code is crash-proof, I still have to consider that bad things could happen. A person might run out of battery as the migration is running. Given enough users, even the unlikely things will happen to somebody.

Here’s what I’m doing. I have two rules:

#### Rule #1: don’t block the main thread

If somebody has a large number of notes on an old device, the migration won’t happen as quickly as expected.

How long before the app would get killed for locking up the main thread? I don’t know the answer — and I deliberately try not to remember how much time I have, not just because it can change, but also because the minute I ask that question is the minute I’m trying to get away with something risky.

It’s entirely likely that I could get away with doing this on the main thread for 99% of users. It would happen so quickly that they’d never even notice. But this is a case where 99% is not enough.

#### Rule #2: make it repeatable

If there has been a partial migration, make it so the migration runs again at the next launch, and make it so that we don’t end up with duplicate notes.

This is fairly easily done.

On completing the migration — and only on completing — does the app set a BOOL in NSUserDefaults that says the migration is complete.

Future runs check that BOOL. If it’s not there or is false then the app runs the migration.

While doing the migration, each note is checked to see if it already exists in the Core Data store. There’s a `uniqueIDv1` property that we look at. If that ID exists in the Core Data store, then we skip it and go to the next note.

This also allows for the weird case where that BOOL I mentioned gets nuked from NSUserDefaults. (I don’t know how this would happen, but I have to assume weird things are possible.) This would result in the migration being run again — which would be harmless and wouldn’t result in duplicates.

<i>Update 9 pm</i>: Feedback from Twitter — Matt Drance, who knows things — [says](https://twitter.com/drance/status/438146511696703488):

>A UD bool is a state bug waiting to happen. Migrate to new-temp.sqlite and rename when finished.

Agreed. Makes sense. There’s a [more general point](https://twitter.com/drance/status/438149939781066752) he also makes:

>This is basically the systemVersion vs respondsToSelector debate. Do you want to trust or verify?

Verify.
