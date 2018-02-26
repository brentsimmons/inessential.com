@title Immutable Model Objects
@pubDate 2014-03-20 18:07:35 -0700
@modDate 2014-03-20 19:23:31 -0700
I’d like to make Vesper’s model objects immutable — [value objects](http://www.objc.io/issue-7/value-objects.html) — but I’m not sure it’s do-able in a reasonable way. I’m writing this up to figure it out.

#### Why do this?

Mutability is a source of bugs. I’m doing syncing, which is difficult, and I should take every opportunity to reduce the possibility of bugs.

However, it’s important to remember that there are always trade-offs. A system with immutable model objects may have other bugs — after all, it must deal, somehow, with changing data.

#### Current Model

Objects are uniqued and cached in an NSMapTable with weak references. The idea is simple: if you make a change to an object in one place, any other place with a reference will get the change, since it’s the same object.

#### Concrete Example

On your day phone, you change the name of the “ice cream” tag to “Ice Cream.” It tells the sync server about the change.

Later, on your night phone, you edit a note with an “ice cream” tag. Syncing updates that one tag object so its name is now “Ice Cream,” and this is reflected in the UI.

The note and tag objects are unchanged except for tag.name.

#### How I might deal with this

Let’s agree to this: in the detail view, when you're editing a note, the VSNote object is mutable: it’s a VSMutableNote. 

Let’s also agree that this is the only time a VSMutableNote appears in the app. (It’s the only mutable data model object of any kind in the entire app.)

So VSTag is immutable, along with everything else. The above scenario happens like this:

Sync server reports name change from “ice cream” to “Ice Cream.” A *new* VSTag object is created.

The VSMutableNote object (referenced by detail view) has a tags array — which includes the old “ice cream” tag rather than the new “Ice Cream” tag. It needs to replace the old tag with the new tag.

I think the simple answer is an NSNotification. (Name TBD.) It would get sent when a new VSTag is created. The VSMutableNote object would then refresh its tags array — it would make sure it has the latest VSTag objects.

With the current system the detail view controller already needs a notification of some kind — it needs to know when any tag.name changes in its tags array, so it can refresh the UI. This is not a big difference.

#### Pause and figure out where we are

We have four model objects: VSNote, VSTag, VSAttachment, and VSTimelineNote.

I think I’ve found that VSTag can be immutable. VSAttachment already is. VSNote can be immutable *except* for that one mutable note referenced by the detail view controller.

(The sync system can use immutable VSNotes, and post a notification when there’s a change. The VSMutableNote held by the detail view can watch for that notification and do the right thing. Similar to how it handles a tag change.)

This leaves VSTimelineNote.

#### VSTimelineNote

The timeline holds an array of these, and no other part of the app (outside of the data layer) references VSTimelineNote.

The way they work now: when a VSNote changes, a notification is sent, and the corresponding cached VSTimelineNote (if there is one) is updated.

This means that the timeline view controller gets those changes automatically, since a VSTimelineNote in the cache is the same object as in the timeline’s notes array.

However, the timeline view controller does need to know about any changes to notes, since it may have to refresh the UI. Which means — just as in the tag/note situation for the detail view — there already needs to be a notification about changes.

When that notification is received, I could replace oudated VSTimelineNotes in the notes array with their updated versions instead of updating values.

I think that completes it: immutable model objects are not only possible (in Vesper’s case) but barely any different from the code that exists now.

#### Fallout

This has the effect of taking out one part of the data layer code: the uniqued-objects cache.

The whole point of that cache is to make it so that all references to a given tag (for instance) are to the same VSTag object, so that when it changes in one place, it’s changed in the other places.

(You may note that this is Core-Data-like.)

But if I’m updating objects by replacing them, then the uniqued-objects cache makes no sense. Which means I can delete some code — and probably gain some performance by not having to maintain and access that cache.

It also means that my detached-copy system — which is to create an immutable object that doesn’t appear in the uniqued-objects cache — isn’t needed. This was used in API calls and the sync system. All objects are detached copies, and I never have to think about whether an object is detached or not, and I never have to make a copy if not.

It also means that I could handle sync merging on the database queue rather than on the main thread queue. This helps ensure that the main thread isn’t blocked for any reason.

Finally, it removes a step in the data layer where I make an immutable dictionary version of an object before passing it to the database queue and saving it.

I think it’s a win, and not much work. I’m going to do it.
