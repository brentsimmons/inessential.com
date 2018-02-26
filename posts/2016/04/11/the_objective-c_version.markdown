@title The Objective-C Version
@pubDate 2016-04-11 13:48:54 -0700
@modDate 2016-04-11 13:51:00 -0700
In [Comparing Reactive and Traditional](http://inessential.com/2016/04/08/comparing_reactive_and_traditional) I linked to two solutions to a specific problem: one in RxSwift and one traditional (but also Swift).

To round things out, a friend of mine wrote an Objective-C version. You can see the <a href="https://gist.github.com/brentsimmons/4873cedd2773318d495e0952f20868bb">main view controller as a gist</a> and you can download the <a href="http://ranchero.com/downloads/Fetcher.zip">entire sample project</a>. (Because it’s not all in the gist.)

My friend writes:

>The rules outlined in Comparing Reactive and Traditional represent the business logic for contacting the server: coalesce requests over a timeout period, coalesce non-unique consecutive requests, and ignore requests shorter than a specified length. If I’ve learnt anything in nearly 30 years of writing software, it’s you don’t want to put business logic in the UI. Working with UI is complicated enough without embedding your business logic there. That’s why the business logic is embedded in the Fetcher object – mostly in the -fetchQuery:error: method.

>Because we’re coalescing calls, having a method with a completion handler isn’t appropriate. One unifying theme in Apple’s use of completion handlers is they are ALWAYS called – either with a result or an error – the block is never just ignored. Because we plan to ignore many calls to our query method based on the business logic, either a property with a handler block or a delegate is appropriate. I chose a delegate, because they still have slightly more historical precedence.

>I inferred from Brent’s implementation the rule that new queries should cancel incomplete queries. I’m not certain whether that’s correct, but it seemed appropriate to prevent responses coming out of order.

<p style="text-align:center">* * *</p>

Also: Jorge Bernal’s post <a href="https://koke.me/2016/04/11/from-traditional-to-reactive/">From traditional to reactive</a> is worth reading — he takes the traditional version to the next level (closer to something you’d actually write), by creating a Throttle object.

He writes:

>There’s no <strong>silver bullet</strong>, and that’s also true for RxSwift, but I believe it can help. I can’t imagine reasoning about all the possible states in a more traditional design.

And:

>I also would argue (although someone might disagree) that any time you use `NSNotificationCenter`, `NSFetchedResultsController`, or KVO, you are already doing some sort of reactive programming, just not in a declarative way.

In the Macintosh Toolbox days we wrote code that polled the event loop via GetNextEvent. Our code examined the event and handled dispatching it to the right place in the app. This was a *huge* pain, and you can be glad if you’ve never had to write code like that.

I first experienced the joy of AppKit when I created a menu item in Interface Builder, wired it up to an action method, and then wrote the code in that action method to handle that specific command.

Responding to events in this way is *far* better than the old-fashioned method. I don’t know if I’d call it *reactive*, though — I’d just go with <a href="https://en.wikipedia.org/wiki/Event-driven_programming">event-driven</a>.

(Even the Toolbox version was event-driven — it’s just that it didn’t help with event *routing*, which is a thing we now take for granted.)
