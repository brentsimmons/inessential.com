@title new
@pubDate Wed May 23 15:48:13 -0700 2012
@modDate Wed May 23 15:48:13 -0700 2012
I’ve been a Cocoa developer for ten years. (Less than some, but more than most.) And whenever I see <code>new</code> in someone’s code, I assume they’re new to Objective-C, that they’ve just gotten here from Java or C++.

But now, because of ARC, I’ve started using <code>new</code> as a replacement for <code>alloc/init</code>, just because it’s more compact.

In other words, I’ll type <code>[NSCache new]</code> instead of <code>[[NSCache alloc] init]</code>.

Total surprise to me.
