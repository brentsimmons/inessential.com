@title Why Use a Custom Notification for Note Deletion
@pubDate 2014-02-25 14:29:17 -0800
@modDate 2014-02-25 14:40:10 -0800
I’ve seen some feedback that suggests I don’t need to use a custom notification for when the sync server triggers the deletion of a note.

In general, it’s best just to watch for model object changes, via an NSFetchedResultsController, KVO, or other means, and then do the right thing.

While I agree with the general case, there are times when that’s not going to do what I want.

Consider again the case of a note displayed in Vesper’s detail view. There are two cases where it might get deleted:

1. User taps the trash button.

2. Sync server tells the app that the note was deleted on another device.

In both cases, the note gets deleted. But what if we want to have different behavior for the second case?

It would be easy to justify the following behavior: if the person is now editing that previously-deleted-elsewhere note, then that person implicitly wants that note *not* to get deleted.

So that note would get un-deleted. (Technically implemented by making a copy of the note with a new ID. The user wouldn’t be able to distinguish that from un-deletion — it amounts to the same thing.)

If I just watched for the note to be deleted, if I just watched the model object change, I wouldn’t be able to distinguish one event from the other. (And I couldn’t make the copy, since it would be too late at that point.)

So I use a custom notification that notifies the detail view that the sync server just triggered a note deletion, and that note is about to get deleted. That gives the detail view a chance to react and do the right thing.

<p style="text-align:center">* * *</p>

Syncing adds a bunch of cases like this. Consider the simple case of what happens when the text changes for a note.

<code>note.text = updatedText;</code>

As with deleting, I have to distinguish between a user-generated change and a sync-server-generated change.

If it’s a user-generated change, then I also have to set note.textModificationDate to the current date. The client then knows it needs to send the change to the sync server.

If it’s a sync-generated change, then I have to set note.textModificationDate to whatever the sync server says it is.

The same pattern holds for a whole bunch of note object properties.

I have not found a great pattern for this. What I do is have methods on the note object like <code>userDidUpdateText:</code> so I can distinguish one change from another.

Let there be no doubt: this is a pain. (But, to be clear, it’s not a Core-Data-specific pain.)

In the happiest world there is no need for custom notifications or methods like userDidUpdateText — I’d just observe model objects in the normal ways and everything would work.

But syncing is the meany. Syncing is why we can’t have nice code.
