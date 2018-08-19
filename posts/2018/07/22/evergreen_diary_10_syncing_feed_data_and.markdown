@title Evergreen Diary #10: Syncing, Feed Data, and Swift 4.2
@pubDate 2018-07-22 13:52:07 -0700
@modDate 2018-07-22 13:55:22 -0700
It’s difficult to write a future-proof schema for Evergreen’s `Feed` object because the needs of syncing systems — and other future features — may require me to add properties I don’t know about yet.

And: different syncing systems might need different properties, and I don’t really want to create an uber-schema which is the union of all of these. (And I don’t want to create a `Feed` protocol, because `Set<Feed>` is then impossible.)

What I *really* want is two things:

* A `Feed` object where I can write `feed.someSyncThing` and `feed.someSyncThing = whatever` *with* type safety and *without* defining `someSyncThing` as a property or part of a database schema.
* A `Feed` object where getting and setting these things gets and sets from a database. Persistence needs to be automatic.

In other words: I want arbitrary dot-syntax gets and sets, and I want automatic database-backed persistence.

Let me tackle these in reverse order.

#### Database

I spent the first seven years of my career programming in UserLand Frontier, which includes a database that can be thought of as a giant nested dictionary. Dictionaries contain key-value pairs — and any value could be another dictionary, right?

It was the same in Frontier, except we called them tables. Tables could contain tables. There was no schema: any table could contain key-value pairs.

Persistence was exactly as easy as that: you could get and set values and tables, delete things, etc., and the whole giant nested dictionary was stored on disk as a database.

This is *exactly* the kind of thing I want backing my `Feed` objects. I want a Frontier-like database with a table called `feeds`, and a subtable for each individual feed (keyed by feed ID). The table (remember it’s like a dictionary) for each feed contains exactly what it needs — including any arbitrary future stuff I haven’t needed or though of yet — and nothing else. No database migrations ever. Just room to grow.

Well — I’ve been working on this for a while, and it’s not quite done, but it’s close. [See ODB](https://github.com/brentsimmons/RSDatabase/tree/master/RSDatabase/ODB), which is part of my RSDatabase framework.

Great! So that’s half the job.

But what about the dot-syntax part? Swift is all about type safety, and being able to refer to `object.anything` seems un-Swift-like, no? I mean, that’s like a *dynamic* thing, right? Isn’t that more suited for those free-range kids who write in Ruby and Python?

#### Surprise!

My ODB code was far enough along that I started to actually revise my `Feed` object to use it and to handle arbitrary key-value pairs. I started by implementing a `subscript` method, so I could write code like `feed[Key.etagHeader] = whatever` — but I just didn’t like the look of it.

I *really* wanted dot-syntax, so I could write `feed.etagHeader = whatever` instead. Something — I forget what — made me vaguely wonder: wasn’t there something about this recently?

There was! Check out [User-defined "Dynamic Member Lookup" Types](https://github.com/apple/swift-evolution/blob/master/proposals/0195-dynamic-member-lookup.md), which was implemented in Swift 4.2 — which I’m using — and which makes me extraordinarily happy.

The gist is this: you can add a `@dynamicMemberLookup` attribute on a type, and then use dot-syntax to refer to any arbitrary data, and then implement a special `subscript(dynamicMember: String)` method (or multiple methods for different types) that gets and sets that data.

This is *perfect*. It means my `Feed` object can be as dynamic as its storage — without losing any syntactic niceness or type safety.

I realize that this new feature was written with the idea of working better with languages like Ruby and Python.

But I’ve long maintained that there are cases where dynamic solutions are appropriate even in Mac and iOS app code, even in code written in Swift.

Given the truth — that different `Feed` objects used with different syncing systems will need to store different data — it just makes sense to make `Feed` schema-less. And the combination of my ODB code and Swift 4.2’s dynamic member lookup feature means I *can*.

(Note: I haven’t finished my updated `Feed` code to check it in yet. I’ll update this post with a link once it’s up.)
