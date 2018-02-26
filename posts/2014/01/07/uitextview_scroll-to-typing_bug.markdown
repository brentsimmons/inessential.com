@title UITextView Scroll-to-Typing Bug
@pubDate 2014-01-07 11:01:54 -0800
@modDate 2014-01-07 11:46:53 -0800
As I’ve said many times, I’m a huge fan of [Text Kit](https://developer.apple.com/library/ios/documentation/StringsTextFonts/Conceptual/TextAndWebiPhoneOS/CustomTextProcessing/CustomTextProcessing.html). It’s a big deal for [Vesper](http://vesperapp.co/). Among other things, it lets us do bolding/un-bolding in a way that didn’t work reliably or efficiently in iOS 6.

But with Text Kit came a new UITextView. The old one was based on WebView, and this one isn’t. That makes it a 1.0 version of UITextView, since it’s a new thing. And it has some [bugs](http://inessential.com/2013/10/04/bugs). (Not surprisingly for a 1.0.)

I’ve been trying to figure out work-arounds for these. I’m making progress.

#### Set the frame, not the contentInset

People Who Know(tm) (Greg Pierce, for one) have advised me not to set the contentInset of the UITextView when the keyboard appears and disappears. Instead change the frame. In my testing this makes a big difference.

It means you don’t get the blurred-out UITextView underneath the keyboard, which is too bad, but that trade-off is easy to live with.

#### Scrolling to show typing

I have this *almost* working. Like a bottle of wine I just can’t manage to un-cork.

From Greg Pierce (again), author of [Drafts](http://agiletortoise.com/drafts/), I have this code:

<code>- (void)textViewDid&#8203;ChangeSelection:&#8203;(UITextView *)textView {</code><br />
<code>&nbsp;</code><br />
<code>&nbsp;&nbsp;[textView layoutIfNeeded];</code><br />
<code></code><br />
<code>&nbsp;&nbsp;CGRect caretRect = [textView caretRectForPosition:&#8203;textView.selectedTextRange.end];</code><br />
<code>&nbsp;&nbsp;NSLog(@"y %f", caretRect.origin.y);</code><br />
<code>&nbsp;&nbsp;caretRect.size.height += textView.textContainerInset.bottom;</code><br />
<code>&nbsp;</code><br />
<code>&nbsp;&nbsp;[textView scrollRectToVisible:caretRect animated:NO];</code><br />
<code>}</code>

You can [download a super-simple sample project](http://ranchero.com/downloads/TVJumpBugAlmost.zip) with this code.

The one place it fails:

1. Tap at the end of the text.
2. Tap Return.

The caret is hidden. Type any other key and it un-hides. But I really, really want the caret to be not hidden right then.

If you look in the console you’ll note that `caretRect.origin.y` is just plain incorrect when you tap Return.

You can tap Return again and then backspace and see the same thing — only caretRect.origin.y will be wrong in a different direction.

*So* close. I can almost taste the wine. If you have any ideas, [please let me know](https://twitter.com/brentsimmons). I’ve tried a bunch of things and I’m willing to try more.
