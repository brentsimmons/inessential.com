@title Vesper, New iPhones, and Editing Fixes
@pubDate 2014-09-17 12:55:47 -0700
@modDate 2014-09-17 12:57:28 -0700
<a href="http://vesperapp.co/appstore">Vesper 2.004 is on the App Store</a>.

The two big changes are support for iPhone 6 and 6+ screens and editing fixes.

Supporting 6 and 6+ wasn’t much work. I had done most of this work before the iPhone announcements, and it was a matter of fixing the couple spots that assumed a 320-point-wide screen. The remaining thing to do was to add launch images for the 6 and 6+. Simple.

The editing fixes were a bigger deal. The first thing is that Apple fixed some bugs in UITextView in iOS 8. Because of those fixes, I was able right away to remove some of our many work-arounds, some of which were a bit heinous. I ended up removing *all* of our work-arounds and starting from scratch.

And I was pleased to find that we needed very few work-arounds — and small ones, well-contained and easy-to-understand, not like the previous work-arounds — to make editing of long notes much, much better. I’m very pleased, and I thank Apple for attending to this. It’s much appreciated.

At the same time, I also learned from a person-who-can’t-be-named a couple of things that seem to help with UITextViews.

* Set allowsNonContiguousLayout to NO on the layout manager. It may be NO by default, but set it to NO anyway.

* Avoid using contentInset — use textContainerInset instead.

So: not a huge release, but a very welcome one. Dealing with editing bugs has been a giant time-suck for me, and I’m so glad to finally get past that, and I think Vesper users will be pleased.
