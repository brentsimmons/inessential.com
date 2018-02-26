@title Core Data Thoughts - June 2014
@pubDate 2014-06-11 12:49:20 -0700
@modDate 2014-06-11 12:59:51 -0700
I’ve been thinking about Core Data since WWDC 2014. I had three feature requests filed with Apple — one each for batch updates, batch deletes, and asynchronous fetches.

They did two of three: batch updates and asynchronous fetches. That’s *huge*.

Nevertheless, it’s still possible to prefer an alternate data layer — but I think it’s harder to <em>justify</em> an alternate model layer.

There are some things I prefer about my own system.

I like that in my system model objects are always main thread objects and all database access is on a background queue, so that the main thread is never, ever blocked. This takes care of concurrency and UI responsiveness issues.

You might say that smart use of Core Data would amount to just about the same thing, and I’d reply that I’m not going to be smart all the time, and so I design my data layer so that it takes care of me when I’m dumb.

I also like that, in my system, model objects aren’t necessarily tied to the database. In Vesper I have VSNote objects where changes get saved and VSNote objects that are detached from the database. One use of this is in syncing: I can generate detached VSNote objects from incoming JSON, and compare those to VSNote objects tied to the database. It’s nice not to have two separate classes.

I like that the IDs for my objects are also primary keys and are defined by me. This matters when dealing with data coming from the web.

I also like using SQL directly. Core Data adds a layer between me and what I want the database to do — and it’s easier for me just to tell the database what to do. Cut out the middle-man.

Here’s an example: I have a query that lets Vesper know if there is at least one unarchived note without a tag. I don’t want the note — I just want a boolean. My query is straightforward and looks like this:

<code>select 1 from notes where archived=0 and uniqueID not in (select distinct noteID from tagsNotesLookup) limit 1;</code>

The Core Data equivalent would be a fetch request that gets any note where tags is nil and archived is NO, limited to one object. While I can write the SQL almost without thinking, I’d have to look up how to write the NSPredicate. (Yes, that’s on me, but I’m talking about *personal* preferences here.)

At some point these things are outweighed by the need to write and maintain less code. They’re outweighed by the possibility that another person might work on the code, and that person is likely to know Core Data, and will certainly *not* know my custom system.

If Core Data *can* do the job, and do it very well, then it’s hard to justify not using it, despite my personal preferences.

That said, it would be dumb for me to take the time to rewrite Vesper’s data layer: it’s working code, and it’s fast, and I’m happy with it.

But were I to start something new, I would use Core Data.

#### Dreaming

I can’t help but think that it might be time for the Core Data team to do a fresh start. Core Data is about ten years old, and it pre-dates GCD and blocks and iOS. While it has adapted well over the years, it’s still a big framework with far more power than any one app will ever use.

Were I starting over, I’d do something lighter — much like Vesper’s system. Something like this:

* Model objects on main thread only. Detached model objects on any thread.

* Database access is async. Background serial queue. No merge policies, because they’re not needed.

* No saving, because changes are streamed to the database. Undo support is left to the developer.

* SQLite only.

* Object IDs are primary keys and are developer-defined. (Since those IDs often come from web services.)

* Wouldn’t shy away from calling itself a database system, because that’s what it would be. It might even allow arbitrary SQL, though NSPredicate would be preferred in general.

* Would retain important features such as object uniquing. The main thread object cache would keep live objects in sync with what’s in the database. Change notifications of some kind are generated. Would handle relationships. Would use the same (or similar) data modeler that Core Data uses.

This is closer to the metal in the way CloudKit is closer to the metal — which is a virtue of CloudKit.

The biggest challenge in the above is faulting. I would limit this to relationships, so that one simple query can’t trigger cascading queries that end up reading in way more objects than are needed. And since a virtue of this system is that it doesn’t block the main thread, relationship faulting would have to be carefully designed so that it’s async but still convenient for the developer. (Tall order, I know.)

Buuuuuuuuuuuuuuuuuut this is just me dreaming. Projecting my own preferences.

But still, if you were starting from scratch in 2014, designing a data layer for iOS and Mac, in the era of closures and GCD and Swift, in the era of CloudKit and web services, how might you do it differently?

Well. As I said, were I starting something new, I’d use Core Data, and happily. No question at this point. But part of me would keep wishing for a fresh start — a la Swift and CloudKit and Metal.

The thing is, these days, fresh starts seem possible. Two weeks ago it didn’t look that way. I have no inside knowledge, though, so getting your hopes up is not indicated. (And, anyway, it’s just me that’s hoping.)
