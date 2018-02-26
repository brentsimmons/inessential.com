@title Device Sizes
@pubDate 2014-08-05 10:16:12 -0700
@modDate 2014-08-05 11:56:28 -0700
In an <a href="http://www.libertypages.com/clarktech/">article on making it in the App Store</a>, Clark Goble says:

>Apple appears to really want people to make reactive design so that one app will adjust for multiple screen sizes. Thus the loss of the extra income for a separate iPad app. I’m sure they’ll allow dual pricing for a while but I’d be shocked if that pricing will last for long. I bet by fall 2015 Apple will begin demanding a single app for all of iOS.

I would think that Apple would strongly encourage developers to publish universal apps. I doubt they’d switch to actually <em>requiring</em> universal apps.

But we should nevertheless shift our thinking about iOS apps in this respect: rather than think of iPhone apps and iPad apps, we should be thinking about iOS apps.

The addition of size classes and adaptability (and <code>UISplitViewController</code> and popovers to iPhones) means that we need to think more like web developers: we don’t know screen sizes in advance.

We shouldn’t even think about different types of devices (iPhone vs. iPad) — instead we should design for adaptability.

This gives Apple the ability to create devices at different sizes. Imagine devices midway between current iPhones and iPads. Imagine even smaller iPhones or even bigger iPads. It becomes just a range of sizes, not two separate families of devices.

Apple has redefined what a good iOS app does. A good iOS app adjusts to any screen size, and doesn’t care (or even know) if it’s an iPhone or iPad. Or something else.

<i>Update 11:30 am</i>: An earlier version of this post said that <code>userInterfaceIdiom</code> was deprecated. I got that from my notes on session 216 — but it appears I was using shorthand with myself. It might as well be deprecated — but it’s not <em>actually</em> deprecated.

Also, <a href="https://twitter.com/pbendersky/status/496718827116568576">Pablo Bendersky wrote on Twitter</a>:

>I’ll go even further: I think bigger devices might default to different font sizes with Dynamic Type.

I’ve wondered why Dynamic Type was so strongly encouraged. That’s a pretty good explanation.
