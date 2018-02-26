@title Standard Controls
@pubDate 2014-07-10 16:56:15 -0700
@modDate 2014-07-10 16:58:42 -0700
Five and even ten years ago, Mac developers would tell you that you can’t release a Mac app that uses standard controls with their standard appearance.

Mac users would look at iTunes and the iLife apps and expect something more like those — and it was impossible to get that look without lots of customization.

Those were the years of brushed metal, wood-grain bookshelves, iTunes-like custom scrollbars, and so on. It seemed as if developers weren’t going for *delight* so much as *awe*. Look at my smoke particle effects and weep, ye mortals.

I think this is changing. A big part — the hugest part — is Apple, with iOS 7 and Yosemite, moving back to consistency and to a design language that looks great, makes sense, and is used by the standard components.

<p style="text-align:center">* * *</p>

There were always problems with creating custom components.

A big one is that accessibility — or *inclusive design* (<a href="https://twitter.com/batalia">Natalia Berdys</a>’s phrase, which I like) — takes more effort. With standard components, you often have to do nothing to get great accessibility. But if you’re building from scratch, you have to do more work than just making it look cool.

Another is that custom components don’t track Apple’s changes and enhancements. One eye-opener: on a recent <a href="http://daringfireball.net/thetalkshow/2014/06/30/ep-086">The Talk Show</a>, my co-worker Dave Wiskus noted that NetNewsWire 3.2 on Yosemite has a translucent sidebar with the correct font, while most Mac apps don’t. This is entirely because the source list was pretty much a standard source list, not because I had some special foresight years ago.

Another example is the activity sheet on iOS. You could create your own (we did, in Vesper) — but you won’t be able to support extensions in iOS 8 if you do.

A big problem is the *cost* of all this development. It makes me think of a recent post by Luc Vandal on <a href="https://medium.com/@lucvandal/the-indie-life-9f968abbdeff">The Indie Life</a>:

>I have spoken with other successful developers and many told me the same: sales are generally down. They are still doing great but there are more and more competitors also taking a slice of the same pie.

It’s probably necessary for indies to make more than just one iPhone app. Do the same app on Macintosh. Maybe make a second or third app.

Not long ago this would have been very, very expensive — because we believed (rightly) that we had to do custom versions of all the things.

But now, I most emphatically suggest getting out of that mindset. Use standard components in the expected ways as much as possible. Create custom things only when absolutely needed.

My app <a href="http://vesperapp.co/appstore">Vesper</a> has a bunch of custom UI. A ton, actually. Could we cut back and still provide a great experience without any impact on the character of the app? Absolutely. And this shows how much has changed since iOS 6 (when Vesper 1.0 shipped) and now.

The things to concentrate on are what an app does, how it works, how it feels to use it, and how responsive and fast it is — which does not include doing built-from-scratch components except when absolutely necessary.

And it *is* still necessary at times. I’m not saying it isn’t. I’m saying that the reflexive attitude that tells us that nothing can be standard needs to become something we remember and laugh at, like pet rocks and bell-bottom jeans.

Here’s how I think about this to myself: the Romantic era, which started with the Delicious Generation and became dominant with the early iPhone apps, has given way to the Modernist era. Grandiosity gives way to sleekness and honesty.
