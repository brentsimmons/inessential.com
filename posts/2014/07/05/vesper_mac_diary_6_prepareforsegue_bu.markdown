@title Vesper Mac Diary #6 - prepareForSegue bug, maybe
@pubDate 2014-07-05 12:57:36 -0700
@modDate 2014-07-05 12:58:53 -0700
This is either a bug, a misunderstanding on my part, or an error on my part. Though I don’t know if this is a bug or not, I decided it was worth filing just in case it’s a bug.

(<a href="rdar://17567823">rdar://17567823</a>.)

You can download the sample project: <a href="http://ranchero.com/downloads/PrepareForSegueTest.zip">PrepareForSegueTest.zip</a>.

Here’s what’s happening:

* It’s an OS X app with a storyboard.

* The window has a containment segue to an NSSplitViewController.

* The NSSplitViewController has two containment segues, one for each split view item.

* <code>prepareForSegue:&#8203;sender:</code> is not called on either the window controller subclass or split view controller subclass. I can verify that both subclasses are in fact used (via an NSLog in <code>initWithCoder:</code> in each).

Is prepareForSegue not meant to be called in these cases? I have little experience with storyboards until now, but I would have expected that it would *always* get called, since it may be necessary for a parent to set some properties on the child, and this seems to be the place to do it.

