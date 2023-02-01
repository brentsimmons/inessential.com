# Maybe Let’s Not Use Protocols Quite So Much

Many iOS developers reach for protocols automatically. A feature isn’t really wearing its production armor unless it’s been fitted with a few protocols.

Protocols provide a layer almost of defense. Protocols make it formal. Protocols button it up and put a lid on it.

This is the way.

#### It’s not the way

Well, sometimes it’s the way. I’ve been using protocols for 20 years, quite happily and with great results.

But protocols can also make a situation overly complex. Consider this example:

You’re writing a module that fetches data from a database. Let’s call it DataFetcher. The details of the database are internal to DataFetcher. No caller has to know that it’s using Core Data or some SQLite wrapper or whatever. The callers just ask for data and get data back.

Let’s assume that it’s a requirement of DataFetcher that you should be able to swap out the database at some point later on.

Seems like an obvious need for a protocol, right? But it’s not.

Remember that the database is internal to DataFetcher. DataFetcher’s public API should not change, but all of its internals can change. This lets you swap the database any time as an implementation detail.

You might still think that it would be handy to have a protocol internal to DataFetcher that hides the concrete database. But why do that? You’d be creating a protocol with exactly one conformance at a time, which is not the point of protocols — and you’d be adding an additional layer.

Remember [Occam’s Razor](https://en.wikipedia.org/wiki/Occam's_razor) — which does *not* say that the simplest solution is best. Not exactly, anyway. It says that “entities should not be multiplied beyond necessity.” To add a protocol is to add an entity that is beyond necessity for solving the problem.

(In general, you don’t simplify by adding things. You complexify by adding things.)

Adding the protocol might *feel* right, but it’s make-work. You could finish the feature faster — and it would be easier to understand, debug, and maintain for your teammates and for future you — if you skipped the protocol-armor-fitting phase.

#### “But Brent, I’ve Got You Now!”

You remind me that DataFetcher might actually need *two* internal databases at once — at some point it may need to do a migration from the old database to the new one, and then you’d need both at that time.

So therefore a protocol, right? It would have two conforming objects, and it would make this code so much simpler!

I’d argue that this is exactly the time you don’t want to hide the databases: anyone reading the code needs to be able to tell which is the original database and which is the destination. Yes, you can do this with good naming, but every bit of extra obviousness in a case like this is good.

(Every migration tends to be, rightly so, an anxiety-causing operation, and we want to be utterly sure we have it right.)



