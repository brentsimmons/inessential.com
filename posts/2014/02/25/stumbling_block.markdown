@title Stumbling Block
@pubDate 2014-02-25 21:50:11 -0800
@modDate 2014-02-25 22:19:50 -0800
<i>Update 10:15 pm</i>: the solution is at the end. (Spoiler: <a href="http://martiancraft.com/">MartianCraft</a> saves the day!)

<p style="text-align:center">* * *</p>

I’m not sure what I’m doing wrong, but you might, since you’ve probably worked with Core Data more than I have. So I’ll write it up.

Vesper’s table view has an NSFetchedResultsController watching for changes to notes. Keep that in the back of your mind.

#### Data migration

The app has a main thread context. The data migration system uses a temporary private queue concurrency context. I use it with performBlock:. (The contexts are *not* parent/child contexts.)

When the data migration is finished, the private context saves. The main thread context then calls mergeChangesFromContext&#8203;DidSave&#8203;Notification (on the main thread, via performSelector&#8203;OnMainThread).

This all appears to work splendidly.

#### Meanwhile, back at the table view…

The table view controller gets the controllerDidChangeContent: message from its NSFetchedResultsController.

Cool — that’s how things should work. The number of fetchedObjects is correct, even. So happy.

So happy until I notice that all the objects have nil properties, with the exception of properties with default values (as defined in the data model).

They are *not* faults, and accessing any of the values (such as note.text) just returns nil. (If they were faults, accessing note.text and so on would work.)

And the table view appears empty.

I don’t know why.

#### Some things I tried

If I navigate to another screen and back, everything works correctly. Properties get their values.

If I use the main thread context for data migration, then I don’t have this problem. (But I don’t want to use the main thread context.)

#### The kicker

It occurred to me that perhaps I wasn’t doing the merge-changes thing properly.

So I put an NSLog in the method that gets that notification, so I could look at the to-be-merged data.

The method looks like this:

<code>NSLog(@"userInfo: %@", [note userInfo]);<br />
[self.mainThreadContext mergeChanges&#8203;FromContext&#8203;DidSave&#8203;Notification:note];</code>

Guess what? *It works then.* The table view is not empty; objects have expected values.

Take the NSLog away, and it doesn’t work.

So then I wondered — what would happen if I take the NSLog away, but set a breakpoint on the remaining line, and do a `po [note userInfo]`.

Well, it works in the sense that po does what I expect — but the objects have nil properties rather than expected values. It does not have the same effect NSLog has.

This is Core Data getting back at me.

P.S. On a hunch I tried one more thing instead of the NSLog: `sleep(1)`. Guess what — it does the trick. Table view is non-empty and the objects have properties with values.

(But of course I can’t leave it that way.)

#### Solution - updated 10:15 pm

Stupid? Embarassing? Sure thing.

I was emailing with the awesome <a href="https://twitter.com/protocool">Trevor Squires</a> (of <a href="http://martiancraft.com/">MartianCraft</a>) about this and he picked it out:

I was listening to the wrong notification. I was listening to <code>NSManagedObjectContext&#8203;ObjectsDidChange&#8203;Notification</code> when I should have been listening to <code>NSManagedObjectContext&#8203;DidSave&#8203;Notification</code>.

Total rookie mistake. (Because I am, in fact, a Core Data rookie.)
