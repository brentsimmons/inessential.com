@title Core Data, Concurrency, and Vesper Tags - Again
@pubDate 2014-02-28 19:59:11 -0800
@modDate 2014-02-28 20:10:01 -0800
I got some great advice from <a href="https://twitter.com/protocool">Trevor Squires</a> and other experts: use a private context that’s just for tags.

Trevor also advised me to think about it this way: in a case like this there should be one authority. One place where tags can be created. (He’s exactly right.) So I created a VSTagAuthority class.

Other advice: I should cache the object IDs (not the managed objects) in an NSMutableDictionary, so I can avoid doing fetches.

So I present VSTagAuthority. It may need some debugging, but it’s pretty close if not all the way there. (Close enough to be illustrative.)

#### VSTagAuthority.h

The ideal API looks like this:

<code>- (VSTag \*)existingTagWithName:(NSString \*)name;</code><br />
<code>- (VSTag \*)tagWithName:(NSString \*)name;</code><br />

(tagWithName creates a tag if needed.)

I came pretty close:

<code>- (VSTag \*)existingTagWithName:(NSString \*)name context:(NSManagedObjectContext \*)context</code><br />
<code>- (VSTag \*)tagWithName:(NSString \*)name context:(NSManagedObjectContext \*)context error:(NSError \*\*)error;</code><br />

If I start embedding gists, this post is going to get huge, so I’ll just link to them: [here’s VSTagAuthority.h](https://gist.github.com/brentsimmons/9283314).

#### VSTagAuthority.m

The init method takes an NSPersistentStoreCoordinator and creates a private context.

Then it fetches all the existing tags and stores their objectIDs in self.tagIDs. (See the fetchTags method.)

Then it implements the API: existingTagWithName and tagWithName.

In both cases it checks self.tagIDs to get the objectID for the tag with that name. If an objectID is found, then it calls objectWithID to get the tag for that objectID and then returns that tag.

tagWithName goes one step further: if the tag doesn’t exist, then it inserts a new tag, saves the context, then stores the objectID in self.tagIDs. (Then returns that new tag.)

Gist-land. [Here’s VSTagAuthority.m](https://gist.github.com/brentsimmons/9283338).

One of the nice things about this is that the private context here doesn’t need to get changes from other contexts. It knows about the tags, and that’s all it knows about, and that’s totally cool.

Another nice thing is that we don’t have to do any locking around access to self.tagIDs, since we use the context’s performBlock(AndWait) methods, which run in a serial queue. (Correct?)

There are also some parts I don’t like. The API doesn’t match the ideal API. But the big thing is that tagWithName can block the caller as it does a database insert, and the caller might be on the main thread. That’s unlikely to be a big deal, but I have to be aware of it.

#### A digression about data

At Seattle Xcoders last night we were talking about Core Data, and [Luke Adamson](http://therecord.co/2014/01/03/luke_adamson) made the observation that most apps could just write their data to a plist using NSCoding.

Core Data — and SQLite — is overkill for many apps that use it.

I could probably get away with this in Vesper for most users. Just hold all the tags and notes in memory, and write to disk on a background queue on changes. (Using coalescing, of course, so it’s not constantly writing to disk.)

If I thought I could get away with this for 100% of users, I’d do it. There’s no need to bring in the relatively heavy machinery of a database just for jazz.

Digression over.

#### After writing this code I went a little squirrelly

I noticed that VSTagAuthority is very, very close to how tags are handled in the shipping version of Vesper, which doesn’t use Core Data.

But, rather than just compare that existing code to this new Core Data code, I decided to write a matching VSTagAuthoritySQL that would do the same thing as VSTagAuthority — except that it would use FMDB/SQLite instead.

I wondered how it would compare.

#### VSTagAuthoritySQL.h

The API matches the ideal API:

<code>- (VSTag \*)existingTagWithName:(NSString \*)name;</code><br />
<code>- (VSTag \*)tagWithName:(NSString \*)name;</code><br />

The init method takes a QSDatabaseQueue (the app’s one-and-only serial database queue) instead of an NSPersistentStoreCoordinator.

[Here’s VSTagAuthoritySQL.h](https://gist.github.com/brentsimmons/9283371).

#### VSTagAuthoritySQL.m

The init method stores a reference to the database queue. It then fetches all the tags and stores the objects in a dictionary. (The actual tag objects, rather than some form of ID, are stored.)

Then it implements the API: existingTagWithName and tagWithName.

existingTagWithName checks self.tags for that tag. If found, it returns it.

tagWithName does the same thing but takes an extra step: if the tag doesn’t exist, it creates a new tag object, caches it in self.tags, then returns the tag.

tagWithName updates the database by adding a block to the serial database queue that does the insert — see insertTagInDatabase.

[Here’s VSTagAuthoritySQL.m](https://gist.github.com/brentsimmons/9283374).

There are some nice things about this. One is that the main thread is not blocked with database access in tagWithName (unless fetchTags hasn’t completed). Another is that the API matches the ideal API. Another is that the implementations of existingTagWithName and tagWithName are very vanilla, plain-jane Cocoa.

There are, of course, things I don’t like. It uses locking, while the Core Data version used a serial queue instead. (But, on the other hand, it can be argued that a little OSSpinLock is simpler than having to use blocks.) Except while the initial fetchTags is happening, those locks will be extremely short-duration, since there’s no database access inside the locks.

I don’t call out the SQL bits as something I don’t like, because I like SQL. But I can imagine many people don’t like SQL. Totally understood.

#### Comparing the two approaches

Both do the same thing in almost exactly the same amount of code. (Though, in real life, some of VSTagAuthoritySQL would be moved into VSTag, as noted in the comments.)

It’s a classic case of trade-offs and values.

The Core Data version wins if you value the things Core Data provides: the data modeler, faults, NSFetchedResultsController, relationships, and so on. It’s an even stronger win if you don’t like SQL. And it wins if you value working with the mainstream Cocoa framework for data — it’s what most everybody else uses, and that’s important.

The SQL version wins if you value its ideal API, its simplicity of implementation, and that it can’t block the main thread with database access (except at startup, while the Core Data version can block on any call to tagWithName). It also wins if you value being able to look at all the source ([FMDB](https://github.com/ccgus/fmdb) and <a href="http://sqlite.org/">SQLite</a>). And it gets bonus points if you actually like SQL. (Which you probably don’t.)

