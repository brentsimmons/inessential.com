@title Core Data revisited
@pubDate Thu Sep 22 15:26:16 -0700 2011
@modDate Thu Sep 22 15:26:16 -0700 2011
I wrote about <a href="http://inessential.com/2010/02/26/on_switching_away_from_core_data">Core Data last year</a>, about how I was switching away from it for one of my apps. The post achieved some notoriety, and to this day people reference it as if I wrote a scathing takedown of Core Data.

Which is not true at all. Here’s what I wrote:

>I bet Core Data is the right way to go 95% of the time. Or more. It’s easy to work with. It’s fast (in most cases). It has schema upgrade tools.

Since that post I’ve used Core Data in other projects. <a href="http://itunes.apple.com/us/app/netnewswire-lite/id418666663?mt=12">NetNewsWire Lite 4.0</a> for Macintosh is a pretty big example of a Core Data app.

At the moment I’m finishing switching <a href="http://glassboard.com/">my current app</a> over to Core Data. (It will still use FMDB + SQLite for a few things, but the main storage will be Core Data.)

This may come as a surprise to people who have it in their head that I’m the guy who doesn’t like Core Data. So I’ll say this — on top of all the other good reasons to use Core Data, here’s another: Core Data is the standard Cocoa object persistence system.

When it gets better, our apps get better. (And it does keep getting better.)

And, more importantly, as the standard it means that <em>any</em> Cocoa developer — a teammate or someone who acquires the app — can jump in and quickly understand how it works.

Yes, your custom thing may be better for your app. But will it <em>stay</em> better? And if you bring someone on to help you, how quickly will they learn your custom thing?

Use Core Data.
