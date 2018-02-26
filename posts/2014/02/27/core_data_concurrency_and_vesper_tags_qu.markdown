@title Core Data Concurrency and Vesper Tags Question
@pubDate 2014-02-27 11:19:24 -0800
@modDate 2014-02-27 11:25:37 -0800
I’m still not sure how to handle this scenario because I’m still learning Core Data and concurrency.

#### The Problem

On your day phone you create a new tag called “Birthday Party.” (You’re planning a birthday party.)

At the same time, the sync server tells your day phone about the “Birthday Party” tag you created on your night phone. (You started planning last night.)

So now you have two tag objects called “Birthday Party,” because your user change happens in the main thread context and the sync change happens in a private queue context.

This is not good. Core Data will not consider this a conflict.

#### Naive solution

My first thought was to have a `tagWithName:` method that 1) finds a tag, and 2) creates it if necessary, then 3) returns a tag object.

The find part is done with a fetch request.

I think — correct me if I’m wrong — that this fails when the tag has been created in Context A but not yet saved, and the fetch request is done on Context B. Context B can’t possibly know about that tag yet.

#### Less-naive solution

So it seems as if a save is needed on Context A before Context B could see the tag object.

If I keep that same `tagWithName:` method and revise it like this:

* Lock it via OSSpinLock. (I hate locks as much as you do, but I’ll use them when it’s the lesser evil.)

* Make it save the context in the case where it creates a tag.

So the method looks like this:

Lock<br />
Do a fetch request for the tag<br />
If not found<br />
&nbsp;&nbsp;Create the tag<br />
&nbsp;&nbsp;Save the context<br />
Unlock<br />
Return the tag

<em>Is this bullet-proof?</em> Will this work as I expect it to?

If there’s a better way to do this, what is it?

(Yes, I realize there’s an optimization where I can maintain an NSMutableDictionary that maps tag names to managed object IDs. I can avoid the fetch request in that case. I’ll do that only if profiling tells me I need it. It doesn’t change the question, though.)
