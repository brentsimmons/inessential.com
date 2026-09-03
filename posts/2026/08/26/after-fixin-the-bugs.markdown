@title After Fixin’ the Bugs
@pubDate 2026-08-26 12:07:54 -0700
@modDate 2026-08-26 12:09:35 -0700

Fixed ’em. Fixed ’em all. Well, almost all — down to 10 bugs on the NetNewsWire bug tracker. (See the [Mac 7.1.3 release notes](https://github.com/Ranchero-Software/NetNewsWire/releases/tag/mac-7.1.3) and [iOS](https://github.com/Ranchero-Software/NetNewsWire/releases/tag/iOS-7.1.3-7206) for the big list of just-fixed bugs.)

This means I’ve gotten the app to the place I’ve wanted to get to for a long time, where the bug count is manageable and close to zero.

So it’s 10 bugs at this writing — and 556 [feature requests](https://github.com/Ranchero-Software/NetNewsWire/issues?q=is%3Aissue%20state%3Aopen%20type%3AFeature). Bug fixing never ends, yes, but the good news is that we can *finally* get going on these feature requests.

## So many feature requests

Some of the feature requests are obviously popular: custom smart feeds, content filtering, thumbnails in the timeline, traditional layout on Mac, and similar.

Other requests are less obviously popular but would be appreciated by a number of people: more syncing systems, appearance settings, sorting options, etc.

Some other requests are very small, would take just one or a few lines of code, and seem like an easy win — like [ignoring elements](https://github.com/Ranchero-Software/NetNewsWire/issues/3501) with the `.instapaper_ignore` class.

There are also the feature requests that are fairly niche, which would be a bit of work and not likely to benefit very many people at all, such as a [horizontally flipped layout](https://github.com/Ranchero-Software/NetNewsWire/issues/5395) or [app-specific proxy settings](https://github.com/Ranchero-Software/NetNewsWire/issues/478). But we consider these seriously too — I’ve been surprised when things like this are *way* less niche than I thought or somehow more important than I guessed.

And these days there are the AI feature requests too, mostly for content filtering and summarizing. We will not be doing any AI features, even local AI features, any time soon. I’m cautious about this kind of thing and I know how difficult it is to remove features, and I don’t know right now that AI is right for this app or how it might be right. We’ll see.

### How do I decide which features to do when?

It’s not as simple as just picking the most popular items and doing those first.

One thing to consider is which features depend on others: for example, showing thumbnails in the timeline depends on adding support for enclosures and Media RSS to the feed parsers, which is a separate feature request, which has its own value besides the thumbnails in the timeline.

(Some feeds — Mastodon feeds, notably — include their images as Media RSS enclosures, which is weird but true, and the article display should show those images.)

Another consideration is NetNewsWire’s job in supporting the web. Which features advance the goal of interoperability and making the web itself the social network? This is why NetNewsWire exists, after all.

Other considerations — besides how many people would benefit, besides the web — include how much work, how hard to test, how risky the changes, and any cognitive and anxiety load it may place on users.

And then there’s also my personal whim! I tend to favor features that existed in NetNewsWire of Yore (NetNewsWire 3.3.2, which we’re still chasing in some ways). Some random feature might compel my attention — maybe it’s an interesting challenge, a thing I’ve wanted to do for 20 years, something I’ve wanted to learn about, or maybe I can’t explain why I want to do it, but I do, and that’s that.

You can follow along if you like. I organize [future releases as milestones in GitHub](https://github.com/Ranchero-Software/NetNewsWire/milestones?sort=due_date&direction=asc). Just note that I make changes all the time — nothing is set in stone until it actually ships.
