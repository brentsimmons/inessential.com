@title A Couple Handy Tricks for Text Measurement Caching
@pubDate 2019-07-26 13:59:05 -0700
@modDate 2019-07-26 14:48:03 -0700
NetNewsWire’s timeline is fast — you can resize it and scroll it quickly.

It has to do a bunch of text measurement in order to do its layout. Text measurement is notoriously slow, though, so we use a cache.

#### How tall is this text?

Let’s concentrate on the issue of knowing how tall some text is. We know the available width (because we know the width of the timeline at any given moment), and we need to know the *height* of some text.

Let’s assume we always `ceil` the height and width and use integers in a `WidthHeightCache` of `[Int: Int]` (width: height). Each string passed to our sizer gets its own `WidthHeightCache`.

The first time it’s asked to get the height for a given width, there’s nothing in the cache, so it has to measure the text and store it in the cache.

And then the second time it looks up the width in the cache — if it’s there, then it returns the cached value. Otherwise it does the text measurement again.

But here’s where it gets smart…

#### Trick #1: in-between widths

Let’s say the first time the width was 100, and the second time the width was 200. Both results are in the cache.

If, on the third call, the width is 150 — between 100 and 200 — *and* the cached height for 100 and 200 are equal, then the height for 150 is necessarily that same height. We can avoid text measurement and just return the cached value. (And we keep the cache from growing on each call.)

#### Trick #2: estimated single-line height

What if, on the third call, the width is 250 instead of 150? There’s another trick. When the sizer is initialized, it can come up with an estimate for the height of a single line of text, just by using a short string (with tall characters) and a very large width.

This estimate means you will be able to know if the cached height for 200 is a single line. If that cached height is suitably close to the estimated single-line height, then you can skip text measurement again and just return the cached height for 200 — since more width can’t make the text higher.

[The code in NetNewsWire for this](https://github.com/brentsimmons/NetNewsWire/blob/master/Mac/MainWindow/Timeline/Cell/MultilineTextFieldSizer.swift) isn’t fully generalized. It maxes out at two lines, since that’s what NetNewsWire uses. But it could form the basis for your own sizing/caching code.

PS Note: this is all because I don’t use Auto Layout on table cell views, for performance reasons. I use Auto Layout everywhere else — just not on table cell views.
