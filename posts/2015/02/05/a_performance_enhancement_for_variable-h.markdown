@title A Performance Enhancement for Variable-Height NSTableViews
@pubDate 2015-02-05 12:02:44 -0800
@modDate 2015-02-05 12:22:55 -0800
Yesterday in one of the several Mac apps I work on I made a performance fix that could be useful to other people.

I have an NSTableView with variable-height rows. The height of the row is determined in large part by the height of the text in an NSTextField.

Unfortunately, text measurement is expensive, and measuring a ton of text as you resize a window causes terrible performance.

One common way to mitigate this is to use a cache so that you never measure the same text twice for a given width. And, in fact, there already was such a cache, so the performance wasn’t as bad as it would have been without it.

I did some testing in Instruments, and it told me that about 20% of the time spent during window resizing was calling the method that calculates row heights.

Then I noticed something about this particular case: quite often the text was just a single line. (Not always, but often. And it wouldn’t necessarily be true for all users. But true enough for enough users.)

So if the height was single-line-height at width n, the height would *still* be single-line-height at width n + x.

I wrote some code that takes that into account — and now Instruments reports that only 0.5% of the time during window resizing is spent in the calculate-row-height method. That’s a nice difference.

#### How It Works

There’s a property, calculated once, called <code>heightForEmptyTitle</code>. It stores the height of an empty string — @"".

There’s also a second cache (an NSCache), called <code>singleLineWidthCache</code>.

The method takes a title (the string to measure) and width.

The first thing to do is to <code>ceil(width)</code> — the title/width/height cache will be nearly worthless unless you round to integers.

Then it checks to see if <code>heightForEmptyTitle</code> has been calculated. If not, it does so.

Then it checks to see if title is nil or @"" — if so, then it just returns <code>heightForEmptyTitle</code>.

Then it looks for a cached height in <code>singleLineWidthCache</code>:

<code>NSNumber *minWidthForSingleLine = [self.&#8203;singleLineWidthCache objectForKey:&#8203;title];</code><br />
<code>&nbsp;&nbsp;if (minWidthForSingleLine) {</code><br />
<code>&nbsp;&nbsp;&nbsp;&nbsp;if (width >= minWidthForSingleLine.&#8203;floatValue) {</code><br />
<code>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return self.&#8203;heightForEmptyTitle;</code><br />
<code>&nbsp;&nbsp;}</code><br />
<code>}</code>

If it finds it, and the passed-in width is greater than the cached width, then we know the height has to be the height of a single line, and we can just return that. (<code>heightForEmptyTitle</code> could also be called heightForSingleLine.)

If it doesn’t find it in the cache, or the width isn’t greater, then it moves on. It looks to see if that title/width combination is in the other cache (the cache that already existed in this method before I got to it). If so, it returns that cached height.

If it wasn’t cached there either, then it does string measurement. (By setting <code>preferredMaxLayoutWidth</code> on the NSTextField and then calling <code>fittingSize</code>.)

If it finds that the calculated height equals <code>heightForEmptyTitle</code>, then it may cache that information in the <code>singleLineWidthCache</code>.

<code>if (titleHeight == self.&#8203;heightForEmptyTitle) {</code><br />
<code>&nbsp;&nbsp;if (!minWidthForSingleLine || width &lt; minWidthForSingleLine.&#8203;floatValue) {</code><br />
<code>&nbsp;&nbsp;&nbsp;&nbsp;[self.&#8203;singleLineWidthCache setObject:&#8203;@(width) forKey:&#8203;title];</code><br />
<code>&nbsp;&nbsp;&nbsp;&nbsp;return self.&#8203;heightForEmptyTitle;</code><br />
<code>&nbsp;&nbsp;}</code><br />
<code>}</code>

If it hadn’t found a previously cached value, or if the calculated value is less than the previously cached value, then it caches the new value.

#### Notes

The code assumes that the height of an empty title is the same as the height of a single line. This isn’t necessarily true (though it was true in my testing). The code is written so that when that assumption is incorrect, the only consequence is that you don’t get this caching. (You don’t get incorrect results.)

It also doesn’t do anything when multi-line text fields are more common. I have an idea for this, though. First look at all the cached height/width pairs for the title. If the passed-in width is between two cached widths that have the same height, then return that height. (In other words, if it has cached width/height 300/26 and 400/26, then a passed-in width of 350 should return a height of 26.) That’s something I still might try.

Also: I mentioned that this is for NSTableViews — but it works as well for NSOutlineView, and it ought to work on iOS as well (though it may be less needed there, since widths are less dynamic).

And it should go without saying that if something that affects text measurement changes — such as the font for the text field — then the caches should be tossed.
