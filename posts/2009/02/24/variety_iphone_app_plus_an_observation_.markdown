@title Variety iPhone app (plus an observation about RSS and technical details)
@pubDate Tue Feb 24 10:58:21 -0800 2009
@modDate Tue Feb 24 10:58:21 -0800 2009
We just shipped a free iPhone app based on NetNewsWire 2.0 — based on our iPhone media app framework, which is the same thing — for <a href="http://itunes.apple.com/WebObjects/MZStore.woa/wa/viewSoftware?id=305013079&mt=8">Variety</a>.

Here’s a screen shot:

<a href="http://itunes.apple.com/WebObjects/MZStore.woa/wa/viewSoftware?id=305013079&mt=8"><img src="http://ranchero.com/images/varietyScreenShotShadow.png" width="330" height="500" alt="Variety iPhone app screenshot" /></a>

#### Hidden RSS

It’s an RSS reader, yes, but nowhere is RSS mentioned on its page on the App Store or in the app.

<a href="http://tumblelog.marco.org/81111782">Marco Ament</a> wrote today, “I think we’ll see more products and features that are based on RSS but don’t <em>call</em> it that.”

Or, as <a href="http://www.micropersuasion.com/2005/11/blogging_enterp.html">Greg Reinacker has said</a>, “RSS is plumbing.”

RSS is so massively useful — it’s how stuff moves around on the web. As technologists we all know how important RSS is. And yet the typical web surfer probably has no idea what RSS is — and they use it without knowing it.

You know what? There’s nothing wrong with that. If it’s plumbing, then cool. Our job as software developers is to create stuff people like. Acronyms and buzzwords don’t mean anything. People want fun things and useful things — hopefully both at the same time.

That isn’t to say RSS readers are going away. They’re not. But a lot of the future of RSS is in doing apps that use it without talking about it.

#### iPhone media app framework

As part of working on NetNewsWire 2.0 I’ve developed an iPhone media app framework. The idea is that, to build an app for a media company, we work with them to gather their artwork, color choices, and a list of tabs and feeds. Then we create a new target with its own configuration file, then build it.

You know what? It works. Good idea. ;) And we have more of these in the pipeline. (In fact our first-to-ship wasn’t this Variety app: it was an app for <a href="http://itunes.apple.com/WebObjects/MZStore.woa/wa/viewSoftware?id=303076023&mt=8">Brad Feld</a> of the <a href="http://www.foundrygroup.com/">Foundry Group</a>.)

Of course, I’m still adding features, on the theory that anything one customers wants will probably be requested by other customers too. And I’m continuing to work on NetNewsWire 2.0. (Many of the requested features will appear also in NetNewsWire.)

#### App design

I have a simple theory about apps like this: they should just work.

While people who use RSS readers always ask for super-fine-grained control over refresh periods and things like that, an app like this <em>shouldn’t even have a refresh button</em>.

That is, there’s no indication that you’re reading RSS. There’s no indication that there are feeds to go out and get. The news just appears.

The app is set so that it refreshes on launch, but only if at least 15 minutes has passed since the previous refresh. In this app, RSS is just plumbing, so I hide the mechanics.

#### Putting pieces together

One thing I seriously love about this app (and the media app framework) is how it puts together different systems we’ve built.

The running app is of course NetNewsWire/iPhone, but it also uses our content service and syncing platform to read the feeds. It provides editorial control over the feeds via <a href="http://www.newsgatorwidgets.com/EditorsDesk.aspx">Editor’s Desk</a> — folks from Variety can pick and choose items to appear in the app.

Editor’s Desk was originally written for widgets (and there is a new <a href="http://blogs.newsgator.com/newsgator_widget_blog/2009/02/new-varietycom.html">Variety widget</a> too) but it works great for iPhone apps like this too.

Using our syncing platform is a cool thing too — because it’s <em>efficient</em>. Instead of reading entire feeds on every refresh, it asks our system just for the new items since the previous refresh. This means the iPhone app is doing <em>a lot less work</em> than it would do were it reading feeds directly from the source.

(It also means the feed provider doesn’t have to concern themselves with a ton of iPhone users suddenly hitting their servers: the app talks to <em>our</em> servers.)

I like it when the pieces come together like this. We’ve spent years building some of these parts, and we get to reap the benefits now.

#### People

And, of course, there are people as well as technologies. I thank the inestimable Ed Manning for putting this deal together. Ed totally rocks.

And I thank <a href="http://twitter.com/walkerfenton">Walker Fenton</a> for all the work he did on getting the product finished.

Especially at the end. We had a deadline, and it was already nighttime when I was trying to finish it and upload it. It went sort of like this:

Me: Oh noes! Can’t ship today! Need -----!

Walker: Oh, relax. Try this -----.

Me: That works. But! Something else! We’re doomed! Need ------!

Walker: Oh, this right here will do the trick. Try ------.

Me: Oh, yeah, good call. But look out! Something else! Halp!!!

Walker: Here’s what to do...

Etc. Repeat until shipped.
