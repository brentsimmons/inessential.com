@title What the Plans Actually Were
@pubDate 2014-04-30 12:30:52 -0700
@modDate 2014-04-30 12:33:55 -0700
This was a long time ago, and it wasn’t necessarily the best plan — but it was the plan.

The last version of NetNewsWire I shipped was NetNewsWire Lite 4.0 for Macintosh. The next step would have been the full (non-Lite) 4.0 for Macintosh, but we sold [NetNewsWire](http://netnewswireapp.com/) to [Black Pixel](http://blackpixel.com/). And Black Pixel’s plans are most likely different from my plans, which is expected and totally a-okay.

Aside from general modernization and performance and memory use enhancements, my big plan was *plugins*.

The idea was pretty simple: make NetNewsWire extendible by other developers. There were already some things developers could do:

* Script the app. (It supports AppleScript.)
* Create custom themes (with HTML, CSS, and JavaScript).
* Create scripted feeds (using AppleScript, Ruby, Python, etc.).

Those were cool features. Not everybody used them, but the people who did use them really liked them. Since NetNewsWire was a productivity-style RSS reader rather than a casual reader, it made sense to add these kinds of features. They were out of the way of the average user, and added a bunch of value for power users.

Along the way I discovered that there was a marketing benefit too. People liked to publish their scripts and themes. And then I’d link to those from ranchero.com. This meant more publicity for the app and it meant people could easily find these extensions that helped them get more out of the app.

This was especially true with themes — because they’re fun to make and fun to try out.

For NetNewsWire 4.0 I wanted to take this to the next level and provide additional ways to extend the app. I got pretty far along in defining some of the plugin types, to the extent that the app was using the plugin API under-the-hood.

Below are the types I was considering. They would all have had Objective-C APIs. And they’d use protocols, so the plugins wouldn’t have had to link to anything.

#### Sharing Plugins

With the explosion of new places to send your content (Twitter, Pinboard, Pocket, and on and on) I realized it would be difficult to keep up and cover everything.

A sharing plugin allowed you to create a user interface (if needed) and to send a URL and text wherever you wanted.

It also would have allowed me to ship plugins outside the normal release process. I could ship a sharing plugin that wouldn’t be included in the standard release, or ship one that could be included later.

These were super-easy to write. Enough was given to you for free that you didn’t have to do much more than configuration plus an http call. (For most cases. And if you needed to do more, you could.)

#### Account Type Plugins

The app would have handled Google Reader and stand-alone feeds itself — but a developer would have been able to add additional types of accounts.

I should describe the planned source list change. Taking a cue from Mail, it would have had zero or more top-level “Google Reader (account name)” folders and one “On My Mac” folder.

Remember that this was 2011, and Google Reader was all most people thought of when they thought of RSS readers. (It would also have had separate sections for smart feeds and scripted feeds. It would have been a more structured source list than in previous versions.)

The idea is that you might have some synced feeds and some non-synced (“On My Mac”), for whatever reason. You might even have multiple Google Reader accounts. (Work and personal, for instance.)

And it was likely that other types of accounts could exist. They might not even be RSS accounts. If a developer wanted to add a way to read Twitter or Facebook, or anything else, that would have been do-able.

While the API for sharing plugins was all the way worked-out, this API was only partly worked out at the time of the sale. But I didn’t foresee any stumbling blocks.

The idea was to make NetNewsWire an app for *all* the various streams of new items.

The native account types — Google Reader and On My Mac — would have used the API. In addition I was planning to support OPML reading lists, and that would have used this API too. (OPML reading lists are cool. Instead of subscribing to a feed, you subscribe to an OPML file on the web, and then your reader reads all the feeds in that file.)

#### JSTalk

Though the above were Objective-C APIs, I wanted to make it possible to use [JSTalk](http://jstalk.org/) for those APIs. I also wanted to support JSTalk in NetNewsWire’s scripts menu.

I considered adding a plugin API for adding other embedded languages. A developer could have added Lua support, for instance. I was on the fence about this one, as it could have meant me going down a rabbit hole.

#### Non-plugin thing

Besides plugins, the other big feature for NetNewsWire 4.0 was the return of the Sites Drawer.

The Sites Drawer, you may recall, was a big outline of feeds you could subscribe to. I had removed it on the theory that it had become pretty easy to find RSS feeds.

*Big* mistake. Discovering feeds was still hard, and there’s a definite value to making that easy inside the app.

It wouldn’t have been a *drawer* this time. It would have been a window (or a view that swaps in to the main view) with a cool UI for finding feeds based on categories. A view with artwork and everything, something great to look at and fun to use.

Unlike the original Sites Drawer — which was built from a plist that shipped with the app — it would have talked to a web service which would have been updated with new feeds regularly.

There would have been a way to suggest a feed or upload your own feeds (anonymously) to the system so that I could look at them and pick out the ones that might interest NetNewsWire users.

Think of something like an App Store for RSS, only designed to fit into NetNewsWire.

(There’s an additional marketing benefit, by the way — we found in the past that when we added someone’s blog, they blogged about it. More publicity for the app. That’s not the reason to do this, but it didn’t hurt.)

#### Special Note About Google Reader

At the time — 2011, remember — I was already concerned that Google Reader might go away. That was part of what made me want to have separate account types and make that explicit in the source list — it would have made it easier to adopt other syncing services.

Rather than make a user switch all their feeds from Google Reader to whatever, they could pick and choose, and it would have been clear which feeds were in which account.

I didn’t have plans to write my own syncing service (I was at NewsGator, and NewsGator had shut down its syncing service). But I did want to support any that came up, and make it so users didn’t face a steep switching cost — they could try out a new service, or many new services, with just a few feeds, and move more feeds over when they felt like it.

Anyway — those were my plans. Very three-years-ago.
