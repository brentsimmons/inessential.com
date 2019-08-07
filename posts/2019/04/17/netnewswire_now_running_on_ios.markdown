@title NetNewsWire Now Running on iOS
@pubDate 2019-04-17 13:22:11 -0700
@modDate 2019-04-17 13:25:38 -0700
[Maurice Parker](https://github.com/vincode-io) took his proof-of-concept code and moved it into the [main NetNewsWire repo](https://github.com/brentsimmons/NetNewsWire) — and now we have a version of NetNewsWire that builds and runs on iOS.

This morning, during my bus commute, for the first time I was able to read my feeds using NetNewsWire on my iPhone. So. Damn. Cool.

<p style="text-align:center">* * *</p>

A TestFlight build is still quite a way away, I think. There’s still a lot to do. You could build it and run it on your own phone right now, but I wouldn’t recommend it yet.

<p style="text-align:center">* * *</p>

I’ve been working on the app for five years. Most of the work is under-the-hood stuff — the UI is always the tip of the iceberg. UI is super-important, obviously, and takes a while to write too, but it’s not the bulk of the code.

Along the way I’ve had many moments where a thing I’d written years before — because I knew I would need it — suddenly becomes useful. For instance, I wrote the OPML parser early on (one of the very first things), and it was only years later when I added OPML import to the app. (There wasn’t even an app at all when I wrote the OPML parser.)

Those moments are *great*. The pieces start to click together, and you realize you planned well.

And this particular moment is one of the greatest of all — because it means that all of that under-the-hood code, written over so long, was ready to run in iOS with just the barest amount of rejiggering. (We needed to deal with NSImage vs. UIImage, for instance. We needed to restructure the workspace tree to make it easier to work on the two apps.)

So: I’m continuing to work on wireframes. We’ll iterate over appearance and behavior using a running app. I’ll get back to working on syncing pretty soon (because it won’t ship without syncing).

<p style="text-align:center">* * *</p>

If you’re interested in helping — testing, coding, giving feedback, helping me think things through, etc. — I’d be happy to invite you to the NetNewsWire Slack group. Just <a href="mailto:brent@ranchero.com">send me email</a> asking for an invitation.
