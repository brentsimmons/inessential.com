@title Core Data and Deleting Objects
@pubDate 2014-02-22 11:11:38 -0800
@modDate 2014-02-22 11:54:52 -0800
The best advice I’ve heard about deleting managed objects is to 1) not do it, or 2) do it only at startup, before any references to those to-be-deleted objects can be made.

Based on this advice, here’s how I’m handling deleted notes in the next version of Vesper:

Notes have a `userDeleted` BOOL property.

When a note is deleted, that property is set to YES.

The various fetch predicates all specify <code>userDeleted == NO</code>, so that deleted notes are ignored. (This is a little ugly, but I accept it.)

At startup, the app fetches all notes where <code>userDeleted == YES</code> and deletes them, before any references could be made.

My questions: is this overly-paranoid? Is there a better way of handling deleted objects?

<i>Update 11:45 am</i>:

Some people on Twitter have suggested listening to contextDidSave.

<a href="https://twitter.com/mgorbach/status/437309887169957889">Gorby</a>, however, warns, “There's no way to ensure safety if you only listen to contextDidSave due to a race.” I’m inclined to listen to him.

<a href="https://twitter.com/rickfillion/status/437307150596317185">RiFi</a> (I just made that up, though he’s probably heard it before) says: that “we broadcast notification about deleting objects when we do it. Anyone with a ref is responsible for dropping the ref.”

<a href="https://twitter.com/pburford/status/437305911749922817">Paul Burford asks</a> if I also wear a belt and braces. I don’t — but only because I’d rather my pants fall down in public than to ship a persistence bug.

The only place I have to worry about this in the detail view. In the timeline view I can rely (I would think) on NSFetchedResultsController to do the right thing. (I’ll find out if I’m wrong.)

But in the detail view it’s possible you could be editing a note while a sync is happening, and the sync server might say that that note was previously deleted. So the detail view needs to do the right thing anyway.

So the better solution, better than what I’d implemented, is as Monsieur Fillion describes: send a notification when a note is about to be deleted. Have the detail view get that notification and do the right thing.
