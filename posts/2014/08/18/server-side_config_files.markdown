@title Server-side Config Files
@pubDate 2014-08-18 11:07:38 -0700
@modDate 2014-08-18 16:41:04 -0700
Brian Schrader, <a href="http://brianschrader.com/archive/changing-app-behavior-server-side/">Changing App Behavior Server-Side</a>:

>…it seems to me that it should be entirely possible to make iOS apps that are mostly configurable from the server-side. This got me thinking. Why not build the app to download its configuration file (i.e. plist, or Localization.strings file) remotely?

With Vesper we use <a href="https://github.com/quartermaster/DB5">DB5</a> for configuring things like fonts, colors, and sizes. What’s stopping us from hosting a DB5.plist on a server, and changing the app on-the-fly?

Nothing. In fact, this is how <a href="http://taplynx.com">TapLynx</a> works. (TapLynx was two-projects-ago for me; I worked on it before <a href="http://glassboard.com">Glassboard</a>.)

TapLynx is DB5’s dad. The product itself was an Xcode project and static library. You’d configure your app using a plist (they were publication-style apps, made of RSS feeds). You’d set colors, graphics, titles, feed URLs, app structure, etc. — all without writing any code.

The configuration file would ship with the app, but the file could optionally include the URL of a configuration file online which the app would download and then use. That file could be changed at will.

The configuration file could also include URLs to graphics, which the app would also download and use. (Think of graphics for tab bar items. That kind of thing.)

We haven’t done anything like that with Vesper because we don’t anticipate needing it. All it takes a server that can host static files (S3, for instance), but it’s still more moving parts, and I’d rather limit the number of things that can go wrong.

And the kinds of bugs this system can fix are limited. It doesn’t change any actual code.

<i>Update 4:40 pm:</i> Folks on Twitter told me about <a href="https://github.com/mattt/GroundControl">Ground Control</a>, Mattt Thompson’s thing, which looks cool.
