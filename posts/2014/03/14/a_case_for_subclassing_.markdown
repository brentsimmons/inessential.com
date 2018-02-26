@title A Case for Subclassing?
@pubDate 2014-03-14 21:42:34 -0700
@modDate 2014-03-14 21:45:00 -0700
[The other day](http://inessential.com/2014/03/08/gocurious) I mentioned that I’m not a fan of subclassing my own classes. But I may have a case where it’s the least-bad option.

Vesper’s timeline view controller has three configurations: all notes, notes for a specific tag, and archived notes.

There are a bunch of properties that are different based on the configuration:

- title
- tag
- notes fetcher (like an NSFetchedResultsController)
- canReorderNotes
- canCreateNewNotes
- searchesArchivedNotesOnly
- no-notes image name

#### To avoid subclassing

I could do a few different things:

- Pass all these to the init method.

- Create a VSTimelineConfiguration object and pass that to the init method.

- Tell the timeline view controller what type it is — VSTimelineTypeAllNotes, VSTimelineTypeTag, VSTimelineTypeArchivedNotes — and add logic to the view controller so it does the right thing based on type.

- Create a delegate for the timeline view controller.

In the normal run of things, I’d just pass all these to the init method. But there are other things the init method needs too, and it’s getting to be the biggest init method I’ve ever written. So that’s out.

Creating a VSTimelineConfiguration object feels a bit like cheating. I’d be creating a whole new class just to make my init method less long. I’m not sure that’s a great trade-off.

Telling the timeline view controller what type it is is distinctly not object-oriented. It means adding some switch statements. That’s out for sure.

A delegate’s not bad, but it makes the whole thing wordy. Methods to implement look like the below, and there are a bunch of them.

<code>- (NSString \*)titleFor&#8203;ListView&#8203;Controller:&#8203;(VSListViewController \*)controller;</code>

The cleanest solution for a delegate is a new class that implements just those methods. (Because the timeline-creating object already has plenty going on already, and I don’t want to add any more to it.) Which means the delegate is just a more-verbose version of a VSTimelineConfiguration object.

#### The argument for subclasses

I’d have three subclasses of the timeline view controller: one for all notes, one for tags, one for archived notes.

I could create a new timeline view controller by specifying the correct class and a small and sane number of parameters to init.

What I like about that: a timeline view controller itself knows everything it needs to know, which means I don’t have to look in multiple places.

#### The argument against subclasses

But of course I really *would* have to look in multiple places, the parent class and the subclasses, as I’m working on the timeline view controller.

And if I didn’t like creating a new delegate or VSTimelineConfiguration object, why would I like creating *three* new objects?

#### Okay, okay

I’ve worked this out by writing about it. (Which is how I work these days.)

I’ve talked myself out of subclassing. I’m going with the delegate. Even though it’s wordier, even though it’s a new object, it’s the best solution.
