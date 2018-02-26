@title Bugs Filed
@pubDate Fri Oct 04 11:25:40 -0700 2013
@modDate Fri Oct 04 12:00:58 -0700 2013
I filed some bug reports with Apple yesterday. Radars.

#### UITextView Bugs

I’ve mentioned before how much I love TextKit. I do. So so much. Crazy much.

I’ve also mentioned that UITextView in iOS 7 is really a 1.0 release, since it’s the first UITextView with TextKit, and so I’m not surprised there are bugs. I understand and forgive — but I’m still eager to see them fixed.

I filed three:

<b><a href="http://openradar.appspot.com/radar?id=5796444913008640">UITextView Doesn’t Scroll to Show Typing</a></b> - <a href="rdar://15148548">rdar://15148548</a>

In Vesper we work around this as well as we can, but it’s not perfect.

<b><a href="http://openradar.appspot.com/radar?id=5741881648480256">UITextView’s selectedRange Is Inaccurate when UIKeyboardWillShow&#8203;Notification Is Posted</a></b> - <a href="rdar://15149060">rdar://15149060</a>

I only care about this one because we work around the first bug by looking at `selectedRange` when the keyboard will be shown. Were the first bug fixed, I wouldn’t care about this.

<b><a href="http://openradar.appspot.com/radar?id=5233494959587328">UITextView Does Unwanted Scrolling When Editing at End of Text</a></b> - <a href="rdar://15149399">rdar://15149399</a>

Vesper users report this bug to us several times a day. What happens is that the text view may scroll unexpectedly when you’re editing a long note. I haven’t found a work-around for this yet.

I filed each of these with a sample project that demonstrates the bug. You can download all three projects in one file: <a href="http://ranchero.com/downloads/UITextViewBugsProjects.zip">UITextViewBugsProjects.zip</a>.

#### UI Feature Requests

The rest of my Radars filed yesterday were feature requests.

<b><a href="http://openradar.appspot.com/radar?id=5715630808367104">Would Like to Set Custom Font for UIAlertView Text</a></b> - <a href="rdar://15145191">rdar://15145191</a>

<b><a href="http://openradar.appspot.com/radar?id=5901448273461248">Would Like to Set Custom Font for UISearchBar</a></b> - <a href="rdar://15145289">rdar://15145289</a>

Since Vesper uses custom fonts for its UI, it’s a little jarring if something appears that doesn’t use the same font. There are just a few places where there is no system support for setting a custom font.

<b><a href="http://openradar.appspot.com/radar?id=5152680854945792">There Should be a Standard Way of Creating Sidebar Menus</a></b> - <a href="rdar://15145462">rdar://15145462</a>

I’m talking about the “basement” menus, often opened by a “hamburger” button. We have one of these in Vesper, and my previous app Glassboard had one too. As do tons of other apps.

At this point it’s become a standard. It solves a real problem. It would be good for iPhone users were there a standard way that these all behaved. (And it would make it easy for developers to match that standard behavior.)

<b><a href="http://openradar.appspot.com/radar?id=5689792285114368">UIScreenEdgePanGesture&#8203;Recognizer Isn’t Forgiving Enough and Isn’t Customizable</a></b> - <a href="rdar://15145539">rdar://15145539</a>

We get frequent bug reports that panning from the left edge of the screen is too fussy. Too easy to miss.

We’re using the standard, new-in-iOS-7 gesture recognizer for this. So I asked that it be made more forgiving or be made customizable.

(Of course, we might be able to work around it by using a regular `UIPanGestureRecognizer`, detecting a screen edge pan, and making it more forgiving than `UIScreenEdgePanGestureRecognizer`. But still, I believe we have evidence that `UIScreenEdgePanGestureRecognizer` should be more forgiving, so I reported it.)

#### PS

My thanks to the folks behind <a href="http://openradar.appspot.com/">Open Radar</a>. It’s a fantastic resource.
