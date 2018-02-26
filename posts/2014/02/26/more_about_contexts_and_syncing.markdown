@title More About Contexts and Syncing
@pubDate 2014-02-26 13:56:25 -0800
@modDate 2014-02-26 14:07:08 -0800
The main idea behind my using parent/background and child/main-thread contexts is to prevent blocking the main thread as much as possible.

#### Digression

The issue of blocking the main thread is one that causes alarm bells to go off constantly in my head as I work with Core Data.

When I write my own persistence engine, I do things in a different way. Like this:

1. Model objects are uniqued and live on the main thread. They exist mainly for the benefit of view controllers.

2. Detached model objects are not uniqued. They’re immutable copies of model objects. They exist for the benefit of API calls, and can be passed around to any thread.

3. *All* database access — reading and writing — is done in a background serial queue. Changes happen in the correct order.

This system has some nice advantages — particularly that the main thread is never, ever blocked by the database. It takes an entire performance issue and tosses it away.

But it has plenty of disadvantages, too. Many of the nice things about Core Data — the data modeler, NSFetchedResultsController, easy handling of relationships, and faulting — don’t exist. (Though I could write some of them, if I wanted to spend the effort.)

So it’s not that, in order to work with Core Data, I have to learn to ignore those alarm bells about main thread database access — instead, I have to pay <em>more</em> attention to them so I can hear which ones are louder.

#### Big Saves

Here’s what I insufficiently considered previously: how much data will the main-thread context be saving?

If it’s saving a bunch of data, then it absolutely makes sense to have the main-thread context a child of a parent/background context. This pushes saves off the main thread.

But it won’t be saving much data. The main thread context gets only user-generated changes — you add a tag, change the text, etc. As long as it’s not saving on every keystroke, as long as there’s coalescing, then it should not be an issue to do saves on the main thread.

<a href="https://twitter.com/floriankugler/status/438769299852120065">Florian Kugler writes</a>:

>Exactly. If the main context only deals with saves from the UI it should be fine without a parent.

So now my thinking that the best thing for my app is to with a setup like this:

1. Main thread context for UI. Independent.

2. Background, private queue context for syncing. Independent.

They share a store coordinator, but there’s no parent/child relationship.

In addition, I’m going to try creating the background context as needed, a new one for each sync session. I don’t need to keep a long-running background context around, particularly given that syncing is random enough that caching doesn’t help that much. (I could be wrong about this; I’ll find out.)

As Trevor Squires (of the great <a href="https://twitter.com/protocool">@protocool</a> Twitter handle) <a href="https://twitter.com/protocool/status/438765937873797120">reminds me</a> (not of this particular setup, but of setups in general):

>If it creates pervasive performance hotspots then you can review. It's not hard to swap strategies.
