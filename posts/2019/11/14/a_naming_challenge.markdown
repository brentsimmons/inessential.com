@title A Naming Challenge
@pubDate 2019-11-14 10:38:41 -0800
@modDate 2019-11-14 10:38:41 -0800
In NetNewsWire, we have a concrete `Feed` type that’s what you expect: it describes an actual web-based feed.

But there are other things that are feed-like in some important ways. Smart feeds, script feeds (in the future), search results, and folders.

They have some things in common: an icon, the ability to fetch articles, the ability to provide an unread count, etc. These common abilities each have a separate protocol: `UnreadCountProvider,` for instance.

But this is so common that we should have a single protocol that bundles these up into one.

The problem is — what should we call it?
