@title Core Data Temporary IDs and Threading
@pubDate 2014-02-21 11:38:31 -0800
@modDate 2014-02-21 14:17:44 -0800
Here’s a case in the in-progress version of Vesper:

Tag objects are always created on the main thread, because tags are usually created via the UI. (There’s a dictionary that stores tagname/tag pairs.)

Dealing with data returned by the sync server always happens in a separate NSManagedObjectContext (private queue concurrency).

During merge I sometimes need to create new tags. I can call the main thread, create some tags, and return managed object IDs.

Those IDs will be temporary IDs sometimes. But the main thread might save the NSManagedObjectContext before the private queue gets the chance to retrieve those tag objects by ID. Which means — I think — that it will fail.

Do I understand correctly?

In other words, is it unsafe to use temporary managed object IDs across threads?

<p style="text-align:center">* * *</p>

<i>Update 11:40 am</i>: It *is* unsafe, I’ve just learned, via email from <a href="https://twitter.com/pgor">Paul Goracke</a> (local Core Data expert).

So I have some options. I’ll figure those out and update this post.

<p style="text-align:center">* * *</p>

<i>Update 12:10 pm</i>: Options. Essentially as Paul laid them out, but rewritten. (Any weirdness is therefore mine, not Paul’s.)

#### Option #1: Create tags using current NSManagedObjectContext

The problem with this approach is that a user could create a tag named “ice cream” at the same moment the syncing code creates a tag named “ice cream.” I could end up with two tags with the same name.

This is not as unlikely as it sounds. Tag names aren’t random. If you’re planning a birthday party, then you might well create duplicate “Birthday Party” tags.

A Core Data merge wouldn’t call this a conflict. Would I need to create some custom validation or a custom merge policy, or both?

I don’t know how to handle this, though I’m sure there’s a way.

#### Option #2: Continue creating tags on main thread

Continue with my current system, but use <code>-obtainPermanentIDsForObjects:&#8203;error:</code> and return permanent object IDs.

I like this because permanent object IDs are safe — I can use those across contexts. (At least, I <em>think</em> this means that the other thread could retrieve the tag, though maybe not — maybe it requires an actual context save.)

What I don’t like is that there might be an error here, and I have no idea how I’d recover from that error.

That error puts the app in the state where the tag object exists, but we can’t tell the other thread about it, so the other thread has to... do something. I don’t know what. Create a duplicate tag? No.

#### Option #3: Don’t use Core Data

Paul didn’t mention this option, but I can’t help but think of it. It’s a trivial matter to unique tag objects and make them thread-safe, and to have a shared NSMutableDictionary (locked with OSSpinLock) that allows fast look-up from any thread.

There would be no duplicate tags; there would be no need to deal with validation or merging. Calling my `tagWithName:` method would always succeed. (It returns an existing tag or creates a new one.)

I keep resisting this option, though, because I really am trying to use Core Data with this app.

Option #1 sounds like the right way to go, since it means that the sync code isn’t coupled to multiple contexts. But I am worried that dealing with merging is a rabbit hole. My worry may be misplaced, however — it might be pretty straightforward.
