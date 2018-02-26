@title WKWebView Workarounds
@pubDate 2017-12-20 15:23:35 -0800
@modDate 2017-12-20 15:25:12 -0800
In <a href="https://github.com/brentsimmons/Evergreen">Evergreen</a> I’m using `WKWebView` instead of `WebView`, because it’s the new and improved WebKit view. <a href="http://nshipster.com/wkwebkit/">NSHipster writes</a>:

>Boasting responsive 60fps scrolling, built-in gestures, streamlined communication between app and webpage, and the same JavaScript engine as Safari, WKWebView is one of the most significant announcements to come out of WWDC 2014.

Sounds great! I’m on board.

One of the best parts about it — easily enough to sell me — is that a crash in `WKWebView` won’t crash my app.

(Back when I was doing NetNewsWire, crashes in the old `WebView` — the predecessor to `WKWebView` — were the most common crash. But, to be fair, many if not most of those were actually Flash crashes.)

I’ve also heard, though I’m not sure how to verify, that `WKWebView` is better for accessibility, too. So it’s a win all around.

#### But it’s not a win all around

`WebView` — good ’ol trusty friend — has a bunch of things that `WKWebView` is missing.

The new web view has no built-in support for finding text, for instance. I’m not sure what I’m going to do about this, since the ability to hit cmd-F and look for some text is a pretty fundamental thing, and I can’t skip it.

It also has no delegate method for when you mouse over a link. Seems like another fundamental thing, right? Any browser offers you a status bar or some way to see the URL of the link your mouse is over.

What I ended up doing there: my article renderer adds some JavaScript that adds event listeners. (See <a href="https://github.com/brentsimmons/Evergreen/blob/master/Evergreen/MainWindow/Detail/ArticleRenderer.swift">ArticleRenderer</a> in the `renderedHTML()` method.) Then I added handlers in <a href="https://github.com/brentsimmons/Evergreen/blob/master/Evergreen/MainWindow/Detail/DetailViewController.swift">DetailViewController</a>: see `viewDidLoad` and the `WKScriptMessageHandler` extension.

This worked fine: now my status bar shows the URL of the link your mouse is over. Cool.

#### Then the issue of scrolling came up

Evergreen’s design includes a key feature: you can go through all of your news just by hitting the space bar repeatedly.

If there’s more to scroll in the web view (the article), it scrolls. If not, then it goes to the next unread article.

This is a coffee-in-hand feature, which is critical for a news reader.

But `WKWebView` provides no access to its scroll view. (*It does on iOS*, yes, but not on Macs.)

The logic goes like this:

	if canScrollDown()
		scrollDown()
	else
		goToNextUnread()

There are two parts to this, and both (I thought) required access to the scroll view.

#### canScrollDown()

Well… JavaScript comes to the rescue again, just as with the mouseover-link handling. I can run a script in the app and get the results — and JavaScript can tell me the content height and the current amount of scrolling. (I already know the frame size, but I could have gotten that via JavaScript also.)

I did this an <a href="https://github.com/brentsimmons/Evergreen/blob/master/Evergreen/MainWindow/Detail/DetailViewController.swift">DetailViewController</a>, in the `fetchScrollInfo` method.

(Unfortunately, this is asynchronous. I expect it to be super-fast, but I won’t know if this is a problem without a bunch of testing. Let’s set that issue aside.)

The `fetchScrollInfo` method creates a `ScrollInfo` struct (at the bottom of `DetailViewController`) that has `canScrollDown` and `canScrollUp` properties.

So that’s how I know if the web view can scroll. Part one of two solved.

#### scrollDown()

I tried making it scroll via JavaScript. It’s super-easy. But it’s not *animated*, and it needs to be. (In Safari, with a scrollable page, hit the space bar — notice how it animates.)

So I did some research and found some JavaScript utilities, some needing JQuery, for animated scrolling.

But do I really want to add that much JavaScript on every single article load? No way. And will their animation match the animation users expect? I strongly suspect it would be noticeably different.

(I write Mac apps. “Noticeably different” is the kiss of death.)

So I did some nerd-sniping, <a href="https://twitter.com/brentsimmons/status/943554673100824576">on Twitter</a> and Slack, to see if anybody had a suggestion that would work.

People had ideas. Nothing worked.

#### Twist ending

So I’m frustrated, and I’m just about to switch back to my old friendly friend `WebView`, because I know it will do what I want.

The voice of another old friend — the guy who mentored me in my early days as a programmer — came into my head, as it often does in these situations.

“What is the *real* problem you’re trying to solve?” asks <a href="http://scripting.com">Dave Winer</a>, in my head.

The real problem is not arbitrary animated scrolling. The *real* problem is that I want to do a page-down exactly the same way it would work if the `WKWebView` had focus and you hit the space bar. Exactly the same animation and scroll distance.

But *not* arbitrary scrolling: just a page-down.

So I think maybe I can spy on the event stream; maybe I can figure it out by seeing what happens when I click in the web view and hit the space bar. Maybe I can post an event that will do the job.

To do so I make an `NSApplication` subclass, which I do (in Swift, of course), and break on `sendEvent`.

But of course this doesn’t work. The app crashes immediately saying it can’t find the `EvergreenApplication` class. (Which is right there! Dude!)

Whatever.

Okay, maybe it’s back to `WebView` after all. Forget `WKWebView`.

Then I do a search in Xcode on `pagedown`, just out of a last gasp of trying — and, forgotten long ago by me, but look: there is a `scrollPageDown` method in `NSResponder` — and `WKWebView` is an `NSView` subclass which is an `NSResponder` subclass — so, could it be? maybe? it might work?

I tried it: sure enough! It works! With animation and everything. It’s *perfect*.

<p style="text-align:center">* * *</p>

So, in the end, the action method is in <a href="https://github.com/brentsimmons/Evergreen/blob/master/Evergreen/MainWindow/MainWindowController.swift">MainWindowController</a> — see `scrollOrGoToNextUnread`.

(It’s a little weird due to the async thing I mentioned earlier. But it does the job.)

And now — after three years of working on this app — I was finally able to go through all my news just by hitting the space bar. Big day for me.
