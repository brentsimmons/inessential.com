@title Vesper Mac Diary #5 - Storyboards and Passing Things Around
@pubDate 2014-07-05 11:13:20 -0700
@modDate 2014-07-05 11:16:23 -0700
I want to pass things to window and view controllers in Vesper for Mac and I haven’t figured out the right way to do it.

Think of “things” as an NSManagedObjectContext, for the sake of picturing what I’m doing and why it’s important.

I’m using storyboards, so I can’t write custom init methods. Window and view controllers are created via nib-loading machinery. It’s not a document-based app.

How do I get an NSManagedObjectContext (for example) from my app delegate to the window and then to the view controllers that need it?

Maybe the question really is this: how does the app delegate know the main window has been opened?

It’s not available as NSApp.mainWindow during <code>applicationDid&#8203;FinishLaunching:</code> or during <code>awakeFromNib</code>. If the app delegate could know that a window’s been opened, it could set properties on its NSWindowController. Then the view controllers could get the context from the window controller. (View controllers don’t have a reference to the window controller, but they could get there via the responder chain.)

I suppose the thing to do is have the window controller post a notification during <code>windowWillLoad</code>. The app delegate would watch for that notification, then set the right properties on the window controller, which would then be available to the view controllers.

But that doesn’t feel right — it feels a bit sneaky. Hidden. Behind-the-back. But it’s the best thing I’ve come up with. There must be a better way.

What’s the better way?
