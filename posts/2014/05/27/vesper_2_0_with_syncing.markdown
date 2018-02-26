@title Vesper 2.0 with Syncing
@pubDate 2014-05-27 11:26:12 -0700
@modDate 2014-05-27 11:26:12 -0700
Vesper 2.0 is a free upgrade — and syncing is free. Update if you haven’t yet, or [go get it on the App Store](http://vesperapp.co/appstore). Be sure to read the [official announcement on the Vesper blog](http://vesperapp.co/blog/vesper-2-0-and-vesper-sync/).

If you follow my blog, you have a good idea of [the work that went into it](http://inessential.com/vespersyncdiary). Writing about syncing was one of the most fun parts of this — and I very much appreciate all the feedback. It made for a better product. Thank you.

One of the things I didn’t write about much, but that I’m proud of, is the performance enhancements. Vesper 1.0 was fast already, and now it’s faster (and uses less memory).

This work was all about getting the data layer — which was rewritten for Vesper 2.0 — just right. (It still uses SQLite plus [FMDB](https://github.com/ccgus/fmdb), as did 1.0.) I ended up writing the data layer of my dreams. This is a thread I’ve been working on for years, from NetNewsWire through TapLynx and Glassboard through Vesper 1.0 to now.

Another thing I’m proud of is how little actual syncing code there is. There isn’t much room for bugs to hide.

And we shipped with no known syncing bugs and no known crashing bugs. (Obviously I’m tempting fate by saying *anything* about bugs.)

#### The Hardest Thing I’ll Have to Do

Writing syncing meant writing a bunch of different pieces. On the client: data layer, API layer, sync merging, sync state management, sync account UI. On the server: data model, API endpoints, sync merging, and a separate site for resetting passwords and account verification.

I knew this would take a long time, in part because I had to learn JavaScript and Node.js. I also knew that I wouldn’t be able to see the app *actually syncing* until it was pretty close to being finished. It had to wait till all the parts were put together.

It required *patience*.

Anything else I might do — Vesper for Mac, for instance — won’t be as difficult as this was. Even were we to write a hypothetical (completely hypothetical) second app with a separate web service it wouldn’t be as difficult, because now I have all this server programming experience I didn’t have before. (And I’ve already got a data layer I can reuse.)

#### Vesper Mac Diary

The Mac version is indeed next. Look for posts on that subject to start soon. Though probably not till after WWDC.

As much as I love writing iOS apps — and I do — the Mac is my natural home. I think of myself as a Mac developer first. The last Mac app I wrote was NetNewsWire Lite 4.0 in early 2011. It’s been over three years. Definitely time to come home.

Vesper for Mac is entirely a UI job. The data layer and API and syncing code already builds for Macintosh. Now, of course, UI is no small thing, not at all — but the challenge isn’t UI plus other things. It’s just that.

Which feels great. I’m *psyched*. (And looking forward to seeing what changes 10.10 brings.)
