@title Evergreen Status
@pubDate 2018-04-09 13:22:52 -0700
@modDate 2018-04-09 13:22:52 -0700
Things have slowed down for Evergreen — but only temporarily.

I had to spend some time turning 50 years old, which was ridiculously good fun. (One day I hope my 11-year-old nephew and I finish the cover of “Smells Like Teen Spirit” we were working on!)

And… my nine-year-old blogging system needed an update, and I just couldn’t stand it anymore, so I rewrote it. It’s nearly finished now — finished enough that I can post to my blog again, at least.

And then I realized that I had kind of a mess with Evergreen and Frontier frameworks. I was thinking about how I wanted Frontier’s hierarchical key-value database (which I haven’t written yet) in Evergreen  — and so, obviously, they should share this framework. And, well, there are a bunch of frameworks they should share.

So I started work on converting over to Git submodules, so that they *can* share frameworks, and so the frameworks can live in their own separate repositories. Which of course also meant learning how Git submodules work in the first place.

And it turns out that Frontier doesn’t build right now, and needs to be updated for Swift 4. But it needs to build before I can tell if I’ve got frameworks-as-submodules set up there correctly.

Anyway — long story short — there’s finishing the blogging system and then doing a bunch of housekeeping stuff.

In other words: it’s infrastructure week! (And will be for a few more weeks, I expect.)

And *then* I’ll be back to Evergreen. It should be just one more push of a few months to get it to 1.0.
