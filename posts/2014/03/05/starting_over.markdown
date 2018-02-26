@title Starting Over
@pubDate 2014-03-05 11:41:26 -0800
@modDate 2014-03-05 11:41:26 -0800
So now I’m *not* using Core Data with Vesper. I hope the people who (quite rightly) like Core Data are not disappointed. I like Core Data too and recommend it.

Consider the below not as criticism of Core Data but as a description of what I personally like. Also consider all the things I’m giving up: faulting, NSFetchedResultsController, the Core Data modeler (I’m using a plist instead), and plenty more.

#### Designing for what I want

Starting over means I could think about what’s important to me in my persistence layer. At a high level, in order, it’s correctness, performance, simple concurrency, low memory use, ease of programming, and flexibility.

The main goal of the design, in other words, is to make it impossible for me to screw up the data. The last few days (since Saturday) I’ve spent writing a new system. This is how it works:

#### Main thread model objects, background serial queue database

Model objects live on the main thread. This makes it easy to use VSNote, VSTag, and so on in view controllers and in syncing.

There is one exception: you can create a “detached” copy of a model object to use with API calls. A detached model object exists on one thread of execution only, is short-lived, and is disconnected from the database. Detached objects aren’t a factor when it comes to concurrency.

When a model object is added, changed, or deleted, updates to the database are placed in a background serial queue.

Similarly, all fetches happen in that same background serial queue.

This way the model objects and database are always in sync, though the database lags slightly behind until its queue is caught-up.

Concurrency is therefore never an issue, and I never, ever have to worry about the main thread being blocked for database access.

The implicit merge policy is always the same: main thread wins.

Why such a simple concurrency model?

Because sync is hard. There’s a lot of data-merging going on, on the clients and in the web app. Merging is the awful part of sync, but it’s unavoidable.

Since I can avoid yet another case of merging (merging across threads), I will. It’s an entire area that can’t have bugs because it doesn’t exist.

#### Multiple object types per table

Vesper is typical of sidebar/timeline/detail apps in that a timeline view object needs only a subset of what the detail view needs.

So I have two objects — VSTimelineNote and VSNote — which both come from the same notes table.

VSTimelineNote has five properties, while VSNote has 14 properties and two relationships.

This is all specified in the data model. (Here’s a [screen shot](http://inessential.com/images/VesperDataModel.png) of the data model.)

#### Primary keys

One requirement: each model object must have a uniqueID property. It can be a 64-bit integer, NSNumber, or NSString.

That uniqueID is also the primary key (unique, not null) for the corresponding table. I *vastly* prefer this to a system where objects have a local primary key that’s separate from its uniqueID.

The problem with systems like that is that duplicates are too easy to create. I want to make it impossible.

An example: a tag’s uniqueID is the lower-case version of its name. (A tag’s name can be edited case-wise, but if it changes otherwise it’s actually a separate tag.)

There’s no chance of creating duplicate tags because their uniqueIDs would be the same, and since uniqueID is also the primary key, I wouldn’t be able to insert that duplicate tag.

Another example: a note is assigned a 64-bit integer uniqueID on creation on your day phone. That same integer its primary key. On the sync server, that note’s primary key is compound (uniqueID, userID). When the note later syncs to your night phone, it still has that same uniqueID, and the night phone uses it as the primary key. So it can’t create duplicate notes.

#### Relationships

All relationships are ordered. (Via a lookup table with parentID, childID, ix, where ix is the order.)

My system doesn’t do inverse relationships, but for my uses that’s not an issue. VSNote has a to-many relationship to VSTag and to VSAttachment, but to get all notes for a tag I have to do a fetch. Which I don’t mind.

When objects are fetched, their related objects are also fetched. This is done as efficiently as possible: for instance, if three notes are related to a given tag, that tag is fetched just once. (If the tag is already cached, it’s not even fetched once. And, in fact, I’m caching all the tags at startup on purpose, since they’re small and there aren’t many of them.)

#### Uniquing

Some objects are uniqued and some aren’t. Not using uniquing is a performance benefit, except when I could end up with lots of instances of what should be the same object.

In Vesper, VSNote and VSTags are uniqued, but VSAttachments aren’t, because a tag can be related to many notes while an attachment can be related to only one note, so it’s unlikely that a single attachment would have multiple copies at once.

(The data model has a per-object `uniqued` boolean.)

#### Caching

Uniqued objects are cached in an NSMapTable with weak references. That means a note is cached as long as there’s a reference to it outside the cache.

Optionally, an object can be cached permanently, and all objects can be fetched and cached on startup. (There are keys in the data model for this. I do both with tags.)

#### Deleting

Deleting n objects (of the same class) takes one SQL call. If the object has relationships, the entries in the lookup tables are also deleted. To delete 10,000 objects, where that object has two relationships, takes 3 SQL calls. (One for its table and one for each relationship’s lookup table.)

Note that this can lead to orphans — there’s nothing like Core Data’s cascading deletes. Orphans are my responsibility.

#### Syncing

Most of syncing happens off the main thread. Networking doesn’t block the main thread, and parsing the JSON return data also happens off the main thread. Fetching data to send to the server happens in the database’s background queue.

Merging data happens on the main thread, but the database fetches to get that data and the database updates to save that date happen in the background.

So, even though model objects are updated on the main thread, the impact is low. It’s all fast, in-memory operations. If I find later that the impact is not low, I can optimize by merging only cached objects on the main thread and otherwise merging data in the background queue. (I doubt this would be necessary.)

#### Flexibility

Model objects implement the QSDataObject protocol. They must have a uniqueID property and may optionally implement awakeFromFetch. They should be init-able via init. They should actually have the properties claimed in the data model.

Otherwise they can be whatever. They are *not* subclasses of some model object class. Creating an object doesn’t hit the database on the main thread, and I can create an object without ever saving it to the database.

Though there is a data model defined in the plist, table and index creation is done via hand-specified SQL. This allows me to exactly tune how the database is constructed. (I especially like being able to specify which things are unique.)

And it allows me to add tables that don’t appear in the data model and that aren’t used by this system. (An example is the deletedNotes table, which is just a single-column table of uniqueIDs that isn’t backed by a model object.)

Finally, because it’s all just FMDB and SQLite, I can do things that step outside of the basic system. I can solve the “RSS reader problem” — I can mark 10,000 items as read all at once with one SQL call. (The only caveat is that cached objects also have to be updated. Which is easy: just a few lines of code. I could easily add built-in support for this kind of thing to the system if needed.)

#### Reuse

I mentioned that the RSS reader problem isn’t an issue with this system: bulk deletes are built-in, and bulk property changes are easy to do.

While I don’t have plans for another app, I like knowing that the system would work well for these two scenarios:

1. User-created and synced data.

2. Web data with some user-created and synced data. (RSS, podcast, and Twitter clients, for instance. Apps like Glassboard and MarsEdit.)

All the apps I’m likely to ever create fall into these two categories.
