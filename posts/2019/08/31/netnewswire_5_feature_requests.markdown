@title NetNewsWire 5 Feature Requests
@pubDate 2019-08-31 12:08:38 -0700
@modDate 2019-08-31 12:08:38 -0700
NetNewsWire 5.0 is a 1.0 app in disguise. 

And so, as expected, we’ve had a ton of feature requests. Most people tend to request one or two features — and there’s a huge variety in these. People want different things.

Nevertheless, there are a few themes we can pick out from what people are asking for:

* More syncing options, especially Feedly support
* iOS app
* Some way to deal with partial-content feeds
* Customization of the article pane (fonts, colors, etc.)
* Traditional view (timeline on top with single lines, article below)
* More sharing options (Instapaper, Pinboard, etc.)
* Customizable keyboard shortcuts
* State restoration
* Localizations
* Hiding read items in the timeline (or dimming them)
* Hiding feeds (in the sidebar) that have no unread articles
* User-created smart feeds

The less-common, more singular requests are for things like specific sorting options — there are lots of different small options that people would like.

People have also asked for things that might surprise you (they surprised me) — for instance, we’ve had a request for monochrome icons for the toolbar. Another request for a Dark Mode that’s *different* from Apple’s Dark Mode. Etc.

#### How We Choose What To Do Next

The first principle is that we can’t lose what we love about the app. We do our damnedest to ship with no bugs, and the app needs to be fast and, most importantly, it needs to feel lighter-than-air.

Whenever you add things — even if the app remains just as fast, even if there are no bugs — you still run the risk of losing that feeling of lightness. One of the quickest ways to lose that feeling is to add a whole bunch of preferences, View menu options, toolbar commands, and other chrome. So we’re going to be very slow to add things like that.

NetNewsWire needs to not become *fiddly*. (Earlier versions of NetNewsWire got way too fiddly.)

There are other questions we ask about a feature before we do it.

* Will it substantially benefit current users?
* Will it bring a number of new users to the app?
* Does the feature depend on something else being done first?
* How much work will it take?
* Does it require resources (such as new icons) that our programmers can’t provide?
* Does the feature really belong in an RSS reader at all?

And, because this is an open source app, there’s another dimension: people. Is someone available? Has someone just shown up who’s eager to work on a specific feature? Those things have an impact on scheduling, too.

The good news is that most of the common feature requests are obvious things to do.

Some examples — not nearly everything, just a few thoughts:

**The iOS app** is in progress. Maurice Parker has been writing it, and it’s coming along very well. Still plenty more to do, and we won’t ship before iOS 13 ships, but it’s happening.

**Adding syncing options** is a definite good thing for the app. Doing the first one (Feedbin) was the big effort, because it required building the infrastructure that makes syncing possible. Once that was done, adding additional services is not super-difficult. (Not _easy_, no. Nothing’s trivial. But at least the infrastructure and patterns are in place.)

We’d like to support all the various services, or at least a majority of them. And we have people working on adding services.

**Customization of the article pane** will most likely work the way it did in older versions of NetNewsWire: we had theme files which included templates and CSS. The app shipped with a few, and you could make your own and use themes other people made.

This feature shipped with NetNewsWire 2.0, and people really loved it. It was fun!

**More sharing options** is an obvious good idea. *Of course* you should be able to send to Instapaper, Pocket, Pinboard, and so on. We shipped with custom support for MarsEdit and the Micro.blog app — mainly because I use those apps. But an RSS reader ought to support as many sharing workflows as possible. That’s one of the core points of the app.

<p style="text-align:center">* * *</p>

Anyway — the above doesn’t cover everything. Don’t take any of the above as gospel about what we’re doing or when, or what we’re not doing. We haven’t planned 5.1 yet! It’s too soon.

There are also features that we want to do that people haven’t asked for, but that we think are cool. 🎸

The take-away from this article should be: we’re being very careful about designing and implementing new features, because we have to make sure NetNewsWire doesn’t lose what makes it special.

But we *are* doing new features, because there are so many things that can make the app even better — we can make it better for current users and we can bring in new users.
