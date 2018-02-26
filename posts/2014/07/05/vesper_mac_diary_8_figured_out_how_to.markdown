@title Vesper Mac Diary #8 - Figured Out How to Pass Things Around
@pubDate 2014-07-05 17:44:11 -0700
@modDate 2014-07-05 17:44:11 -0700
Let’s pretend the app delegate creates an NSManagedObjectContext, and it needs to somehow pass that context to various NSViewControllers.

Since I’m using storyboards and everything loads automatically — all code-free — I don’t have a code path I can use to send the context around.

I could just cheat. I could use a bit of baling wire in the form of <code>NSApp.delegate.&#8203;context</code> to get that context from anywhere. I’ve done that kind of thing, and I’ll do it again, but I don’t like it. It’s wrong.

The real trick was going from the app delegate to that initial window. Here’s what I figured out:

* App delegate has a lazy managedObjectContext property. Created on demand. (Can’t wait till <code>applicationDid&#8203;FinishLaunching:</code> to create the context, for instance, because that’s too late.)

* NSWindowController subclass for the initial main window posts a window-loaded notification in <code>awakeFromNib</code>. The object of the notification needs to be that window controller.

* App delegate watches for that window-loaded notification. When it gets it, it does the equivalent of <code>notification.&#8203;object.&#8203;managedObjectContext = self.&#8203;managedObjectContext</code>. That sets the context on the window controller.

* The window controller can then pass the context on to its contentViewController, also a subclass. The content view controller can then decide which of its child view controllers need the context, and so on until finished.

I don’t love this. It means the window controller and its view controllers can’t really do their setup until they get that context. But it’s not terrible, and it follows the principle of messages-leafward/notifications-appward.
