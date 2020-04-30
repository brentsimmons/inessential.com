@title NetNewsWire Code Layout
@pubDate 2020-04-29 19:37:14 -0700
@modDate 2020-04-29 19:37:14 -0700
I don’t claim that this is a beautiful diagram, and it might scale weirdly, but it does show how NetNewsWire is layered.

<img src="https://inessential.com/images/NNWCodeLayout.png" width="100%" />

When writing an iOS or Mac app — or an app that’s both, as in this case — I like to 1) break up the app into separate components, and 2) make those components depend on each other as little as possible, and 3) when there are dependencies, make them clear and sensible.

#### Submodules

Starting at the bottom level are the submodules: RSCore, RSDatabase, RSParser, RSTree, and RSWeb. These are built as frameworks: RSCore.framework and so on.

Each of these is in a standalone repo and is useful on its own. They don’t even depend on each other — they don’t depend on RSCore, for instance, though you might have expected that they do.

The lack of dependencies promotes reuse — not just by me, among my projects, but by other people too.

It also makes these easier to work on. I don’t have to worry that a change in one affects another one. I don’t have to pull the latest RSCore before working on RSDatabase, for instance.

In NetNewsWire we treat these as Git submodules. It would be great to switch to Swift Package Manager, but I’m not sure if that has all the features we need yet. (Maybe it does. If so, then great, but there’s no rush.)

#### In-app Frameworks

We continue our bias, inside the app itself, toward using actual frameworks.

The bottom layer is Articles.framework, which is the data model for articles, article status, authors, and so on. Articles depends on nothing else in the app.

ArticlesDatabase.framework and SyncDatabase.framework depend on Articles. ArticlesDatabase stores actual articles data; SyncDatabase stores data used to implement syncing.

The last in-app framework is Account.framework, and it depends on everything below it. An Account is what you think it is: it’s an On My Mac (or iPhone or iPad) account or it’s an account that connects to a syncing system (such as Feedbin or Feedly). It’s at the top of the data storage — to fetch articles for the timeline, for instance, the code asks an Account.

All of these in-app frameworks — like everything in the actual app — may depend on the submodules.

#### Shared Code

Here live a number of controllers that do various things like OPML import and export, downloading feed icons and favicons, rendering articles, handling user commands and undo (such as mark-all-read).

Some could be broken out into yet more in-app frameworks. (We would be more vigilant about that if we felt, at this point, that we’re losing the battle against app complexity. I’m glad to say we’re not in that position.)

#### UI Code

NetNewsWire is a Mac and iOS app. It’s built on AppKit on Macs and UIKit on iOS (as opposed to using Catalyst, which would have let us use UIKit for both).

As the diagram shows, there’s a lot of code shared between the platforms, but that stops at the UI code. The UI level is the top level, and it depends on everything below it.

#### Why use actual frameworks?

The benefits of components and being careful with dependencies are clear — but why use actual frameworks? After all, a conceptual module doesn’t have to translate to an actual separate library target.

I’ve found that it’s easier, when using a framework, to ensure for a fact that you don’t let an unwanted dependency to slip in. It’s kind of like treat-warnings-as-errors — it makes sure you’re not getting sloppy with dependencies.

Other reasons: when I’m working on a framework, I find it easier to just concentrate on exactly what I’m doing there and let the rest of the app slip from my mind temporarily. And, finally, we’re more likely to write tests for frameworks.

It may just be psychology, but it’s important anyway: smaller, self-contained (or mostly so) things are just easier to treat well.
