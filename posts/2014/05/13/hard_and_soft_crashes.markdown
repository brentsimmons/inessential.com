@title Hard and Soft Crashes
@pubDate 2014-05-13 12:06:12 -0700
@modDate 2014-05-13 12:08:14 -0700
I asked what makes a crash a *hard* crash instead of, I suppose, a soft crash. I really had no idea.

Matt Christensen [replied on Twitter](https://twitter.com/_mchristensen/status/466051150098096130):

>I think a “soft crash” is preceded by a hang or other indication of a problem. “Hard crash” is boom, app gone.

Ah. Got it.

A soft crash must mean that somehow the app is either 1) trying to recover, and doing so badly, or 2) eating the exception, even though it means things are screwed up, and limping along for a little while before finally crashing.

Soft crashes are very, very bad. You always want a hard crash — there’s an unhandled exception and the app is gone, right away, no waiting. No chance to further screw things up.

One thing: I tend not to use try/catch. There are none in Vesper. If I’ve made a mistake, I want to shut down the app, get a crash log — or, better, steps-to-reproduce — and fix the bug.

(One random caveat. I haven’t used NSXMLDocument in years, but its initWithData method can throw an exception, even though the documentation doesn’t mention that. If I still used it, I’d have to use try/catch.)
