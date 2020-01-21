@title Uniform Type Identifier Bug on iOS — and How It Affects NetNewsWire
@pubDate 2020-01-20 17:15:46 -0800
@modDate 2020-01-20 21:16:46 -0800
In NetNewsWire you can import your subscriptions from an OPML file. This is the standard way RSS readers work: you can export your subscriptions as an OPML file, and then import them into a different RSS reader.

This way you can move from reader to reader without having to redo your subscriptions list. It’s a good thing.

But in NetNewsWire for iOS (currently in beta) this sometimes doesn’t work because, for some people, the system won’t let you select an OPML file to import. (This does not happen on Macs.)

#### Here’s What Happens

In our app, we declare an OPML type: `org.opml.opml` with a file suffix `.opml`.

The `org.opml.opml` part is a Uniform Type Identifier (UTI), which is Apple’s way of defining document types.

When the user wants to import subscriptions from an OPML file, the app presents a document picker, and the app tells the picker that the user can select files of type `org.opml.opml.

We don’t want the user to select, for instance, a plain text file, or a Pages document, or a GIF, or whatever. We just want to make OPML files selectable.

This works great — except when, for some people, it never works: it doesn’t allow them to select OPML files, and so they can’t import their subscriptions.

It took a while to figure out the problem, but we did.

#### Here’s the Problem

We found that if a user has another app that declares an OPML UTI — and that UTI doesn’t match ours — then the document picker will not see those OPML files as the type we accept (`org.opml.opml`) but as something else.

So far we’ve found two other definitions for OPML: `com.reederapp.opml` and `unofficial.opml` (from Overcast). (To be clear: Reeder and Overcast are tremendous apps, and this situation is not at all their fault.)

For someone with one of those apps installed, the system sees a `.opml` file suffix and decides the file is of type `com.reederapp.opml` or `unofficial.opml`. Which doesn’t match our type — `org.opml.opml` — which means the user can’t select the file. Even though the file suffix is `.opml`.

#### One Possible Solution: Declare All the Types

When presenting the document picker, we could declare that we allow `com.reederapp.opml` and `unofficial.opml`.

But here’s the rub: those are just the two we know about. We would need to do research on all the RSS readers, podcast players, and outliners to find *all* the various declarations of the OPML type.

And, furthermore, every time a new declaration appears in a new app we’d have to add support for that one too. (In the meantime, it would break subscriptions importing, for people with that app, until we do add support.)

#### Another Possible Solution: Tell the System that All Text Files Are Selectable

We could just let the user select any file that’s a text file. OPML files are text files, after all.

But then, so are HTML pages. And Markdown files. And any plain-text documents you may have.

This breaks the principle that you let users select *only* the kind of file that’s appropriate.

But that’s the solution we’re going with. I don’t like it. I’m not even completely sure it will work in all cases, but I am sure that it makes for a sub-par UI.

I don’t see that we have a choice. Please tell me if I’m wrong!

PS We found a related bug report for this from 2012: [Apps can declare bad UTIs that redefine what a file extension conforms to](http://www.openradar.me/10778913).
