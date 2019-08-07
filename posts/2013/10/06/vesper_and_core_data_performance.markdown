@title Vesper and Core Data Performance
@pubDate Sun Oct 06 21:42:53 -0700 2013
@modDate Sun Oct 06 21:53:43 -0700 2013
I mentioned in a <a href="/2013/10/05/vesper_sync_diary_2_core_data">previous post</a> that I was probably going to switch Vesper to Core Data, but that I needed to test with a large number of notes first to make sure it still performed well.

Here’s the test: how long does it take for the All Notes view — the default view, what you see on launch — to show notes?

This view stresses the persistence layer the hardest, since it has to fetch all the notes that have not been archived. (It’s possible in real life that the Archive view could be larger, but with my test data that’s not nearly the case.)

#### Results

I’m using Core Data and <code>NSFetched&#8203;Results&#8203;Controller</code>, running on an iPhone 5.

Here’s how long it takes for my normal (non-test) notes to load: 0.0065 seconds. Excellent.

Here’s how long it takes to load 32,007 notes: 2.6 seconds.

The thing is, the main thread is also blocked for that entire time. My FMDB/SQLite version doesn’t block the main thread (except for an imperceptible amount of time). However, my FMDB/SQLite version takes longer to show data.

#### The Choice

I see two options:

1. Optimize my FMDB/SQLite version further so that it can do fetches in batches. (I’d already done some of the work on this, so it’s not as bad as it sounds, but it’s work I’d rather not do, since I’d rather be <a href="http://daringfireball.net/2013/09/vesper_whats_new_whats_next">working on syncing</a>.)

2. Assume that people aren’t going to hit tens of thousands of notes for a while, and in the meantime iPhones will get faster. (This same test probably runs faster on an iPhone 5S, after all.)

To be clear: I don’t like, at all, that it takes 2.6 seconds for 32,007 notes, and I especially don’t like that the fetch blocks the main thread. But at this point I’m willing to say that my own productivity is more important than getting that 2.6 seconds down to something smaller.

What if that number had been 10 seconds? I wouldn’t make the same trade-off — I’d go back to FMDB/SQLite. That might have been true for 5 seconds too. But for 2.6 seconds I’ll make this trade-off and stick with Core Data.

Whew.
