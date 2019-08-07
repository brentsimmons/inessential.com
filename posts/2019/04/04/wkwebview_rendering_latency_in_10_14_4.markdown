@title WKWebView Rendering Latency in 10.14.4
@pubDate 2019-04-04 13:16:16 -0700
@modDate 2019-04-04 13:16:16 -0700
I noticed, starting in MacOS 10.14.4, that switching between articles in NetNewsWire was way less smooth than it had been.

NetNewsWire uses a WKWebView to display HTML. Before 10.14.4, there was no perceptible delay when switching to a new article.

With 10.14.4, there is. It’s quite noticeable, enough to be unacceptable.

I did some more detective work, and I’ve narrowed down the problem a little bit.

I’m using `loadHTMLString(String, baseURL: URL?)`. The HTML is generated locally, and I set the `baseURL` because I want relative paths (especially for images) to get resolved properly.

What I found:

* If I make `baseURL` nil, then the latency is gone.
* If `baseURL` is the same as in the previously-loaded article, then the latency is gone.

#### Probable workaround

Here’s what I’m exploring: instead of using `loadHTMLString` for each article, I will:

* Call `loadHTMLString` with a nil `baseURL` exactly once, to load a template.
* To make relative paths resolve, I’ll parse and rewrite article HTML with resolved relative paths.
* To load a new article, I’ll pass data to a JavaScript function inside the template that will swap-in new HTML in the right places (title, body, byline, avatar, etc.).

This is not work I was planning, and it means taking a break from syncing to get this done — because, right now, with 10.14.4, the app is not nearly as nice to use as it was.

PS While I’m rewriting the HTML, I’ll also [remove `ping` attributes](https://lapcatsoftware.com/articles/Safari-link-tracking.html).
