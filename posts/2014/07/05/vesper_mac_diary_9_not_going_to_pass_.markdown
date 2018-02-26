@title Vesper Mac Diary #9 - Not Going to Pass Things Around
@pubDate 2014-07-05 21:19:02 -0700
@modDate 2014-07-05 21:19:02 -0700
Having gone to the trouble of figuring out how to pass an NSManagedObjectContext (or equivalent) from app delegate out to an NSWindowController and its NSViewControllers, I think I’m not going to do it.

Or, not entirely.

The benefit of passing things around is less-tangled code, which promotes code reuse and testing and makes for easier maintenance.

But there are three things to consider:

* Passing things around <a href="http://inessential.com/2014/07/05/vesper_mac_diary_8_figured_out_how_to">requires more code</a>. It’s less simple than, for example, just calling NSApp.delegate.context.

* I never reuse view controllers, and I don’t write tests for them. I might some day do automated UI testing, but that runs against the app, not against a view controller in isolation. (I do test other things.)

* I’ve never had a case where a view controller wants something other than the global version of whatever-it-is.

I may sound like a short-sighted, non-OO monster at this point. Here are a couple mitigating points:

* A view controller’s data source and helper objects *should* take a context (and whatever else) as an initWith parameter. And the data source and helper objects should be tested, and may very well be reused. So, even though a view controller may refer to NSApp.delegate.context, its (testable, reusable) helper objects won’t.

* If I’m wrong, revising a view controller to take a passed-in context (or whatever) isn’t difficult.

So that’s there where I am. (Slowly and obsessively questioning everything, as usual.)
