@title On the Many NetNewsWire Feature Requests to Show Full Web Pages
@pubDate 2019-09-04 22:25:07 -0700
@modDate 2019-09-04 22:30:14 -0700
A number of people have asked that NetNewsWire show the full web page — right there, in the app — after clicking a link.

The idea is pretty good! It solves two big problems:

* You get full content, which is great when a feed contains only summaries or truncated articles
* You don’t have to switch to another app: you can stay right where you are

You’d think it’s a no-brainer, and we should just go ahead. But there are other considerations.

One big one is that your ad blockers and privacy extensions won’t run. They work in Safari, but they do *not* extend to other apps that use WebKit. This means that viewing a web page in NetNewsWire would be less secure and more annoying than viewing the same page in Safari (or whatever your browser is).

This points to one of my design principles: the app should have boundaries. Some features belong in the app, and some features are best left to apps that do that feature way better than NetNewsWire could. One of those things is showing web pages — that’s really a web browser feature.

Having boundaries means we can concentrate on doing a great job at the things that do belong in the app.

(Before you mention [SFSafariViewController](https://developer.apple.com/documentation/safariservices/sfsafariviewcontroller), recall that it’s iOS-only.)

#### What about the glory days?

“But Brent! In NetNewsWire 2.0 you added a tabbed browser to NetNewsWire, and it was awesome and a hugely popular feature!”

It was! But times have changed. Many websites are hostile these days. In 2005, this feature was fine — but these days it’s totally not.

#### A winged messenger arrives with a solution

There *is* a solution to the problem of showing full content and not leaving the app, and it’s a feature that really *does* belong in an RSS reader: using content extraction to grab the article from the original page.

If you’ve ever used Safari’s Reader view, then you know what I’m talking about. The idea is that NetNewsWire would do something very much like the Reader view (but inline, in the article pane), that grabs the content and formats it nicely, without all the extra junk that is *not* the article you want to read.

There are a number of open source options for this. We’re looking at using [Feedbin’s content extraction service](https://feedbin.com/blog/2019/03/11/the-future-of-full-content/) (which wouldn’t require you to have a Feedbin account).

The generous folks at Feedbin are running a copy of the open-source Mercury Parser, and they’ve offered to open this service up to RSS readers like NetNewsWire. ([Reeder](https://www.reederapp.com/) uses it already, for instance.)

#### When?

Right now we’re working on NetNewsWire 5.0.1, which is (almost entirely) a bug-fix release. I don’t know what’s going to be in 5.1 yet — we’re still digesting all the feedback, looking at our original roadmap, and thinking about things.

We’re also working on NetNewsWire for iOS! We’re busy.

But this is definitely the kind of feature that should come sooner rather than later.
