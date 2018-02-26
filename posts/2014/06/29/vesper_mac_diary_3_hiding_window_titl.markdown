@title Vesper Mac Diary #3 - Hiding Window Title
@pubDate 2014-06-29 20:32:46 -0700
@modDate 2014-06-29 20:35:38 -0700
I wanted to try that new thing where you can hide the window’s title bar.

I have a window with a toolbar in a storyboard, so the first place I looked was in Interface Builder. I didn’t see anything there for setting this property.

No big deal. (<a href="rdar://17501388">rdar://17501388</a>.) Some things don’t make into IB, or they make it later on. Easy enough to do in code.

So I created an NSWindowController subclass and assigned it to the window controller in my storyboard.

Then in `windowDidLoad` I added the following line:

<code>self.window.&#8203;titleVisibility = NSWindowTitleHidden;</code>

That should do it. But it didn’t — windowDidLoad doesn’t get called. (At least for storyboards, or at least for this one.) (<a href="17501206">rdar://17501206</a>.)

Next I created an `awakeFromNib` method and added that same line of code there. It worked! In case you’re wondering how to do this, now you know.

#### Special note about Swift

I’m not writing code in Swift, just because when things go wrong — as they did above — using Swift adds an additional element of uncertainty, since Swift isn’t shipping yet.

(I *wish* I were writing in Swift, because it looks like fun. I’ll wait.)

But I did make a classic mistake right at first:

<code>self.window.&#8203;titleVisibility = NO;</code>

This translates to <code>self.window.&#8203;titleVisibility = NSWindowTitleVisible;</code>, which is not what I meant.

Would Swift have caught this bug for me? I suspect it would have.
