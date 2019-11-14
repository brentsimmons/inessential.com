@title A Naming Challenge
@pubDate 2019-11-14 10:38:41 -0800
@modDate 2019-11-14 10:44:31 -0800
In NetNewsWire, we have a concrete `Feed` type that’s what you expect: it describes an actual web-based feed.

But there are other things that are feed-like in some important ways. Smart feeds, script feeds (in the future), search results, and folders.

They have some things in common: an icon, the ability to fetch articles, the ability to provide an unread count, etc. These common abilities each have a separate protocol: `UnreadCountProvider,` for instance.

But this is so common that we should have a single protocol that bundles these up into one.

The problem is — what should we call it?

<p style="text-align:center">* * *</p>

Maybe the right for that single protocol is `Feed`. If so, then what should we call the concrete type for web-based feeds?

<p style="text-align:center">* * *</p>

In the original design for NetNewsWire, five years ago, `Feed` was going to be a protocol. Then I started working in Swift, found that I wanted to use `Set<Feed>` and couldn’t, so I made it a concrete type.

I love Swift, but this limitation keeps coming up for me. I use both protocols and sets a lot, because they’re often the best choice, but in Swift they just don’t play together well.
