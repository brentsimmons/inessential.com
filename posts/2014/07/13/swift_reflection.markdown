@title Swift Reflection
@pubDate 2014-07-13 12:03:07 -0700
@modDate 2014-07-13 12:11:01 -0700
When I wrote about <a href="http://inessential.com/2014/07/12/swift_structs_and_valueforkey">Swift structs and valueForKey</a> yesterday, I didn’t know of a way to get this behavior.

Then Jason Peebles <a href="https://gist.github.com/peebsjs/9288f79322ed3119ece4">posted a gist</a> showing how to do it. (Don’t be blinded by the fact that it’s doing operator overloading. The body of the function is what’s important.)

Though it’s not documented in the <a href="https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/SwiftStandardLibraryReference/">Swift Standard Library Reference</a> — and is subject to change, and could disappear entirely — Swift has a reflection API.

I wouldn’t build anything on it, myself. It’s one thing to use documented features knowing that they could change — but using undocumented features is just asking for trouble.

But still, it’s interesting.

The Objective-C runtime has methods for getting lists of properties and methods and other info about objects — but they’re C APIs and they use C types, so they’re not that nice to deal with.

And, given the general guideline that <code>#import &lt;objc/runtime.h></code> in production code is almost never a good idea — and given that Cocoa has valueForKey:, setValue:forKey:, performSelector:, and respondsToSelector: — the Objective-C reflection APIs are (as far as I can tell) rarely used.

This is by design, surely. And you can imagine why: using reflection is a great way for  developers to have fun while making clever and hard-to-understand systems.

But here’s the thing: I want this. It has its uses. And, used well, it can make for simple and easy-to-understand systems that are easy to maintain.

I forget who said that Swift is a language that can *use* something like Core Data but where you couldn’t actually *implement* something like Core Data. You might have solid reasons for wanting to look at an object’s properties (to write a generic JSON serializer/de-serializer, for instance). You might want to be able to provide method implementations at runtime, as Core Data does with @dynamic properties in Objective-C.

If I had to guess, I’d say we won’t see much of this in 1.0. It’s an advanced feature, not very safe and very open to abuse, and Swift needs to focus on safety for its first release.

But before too long we’re going to need this stuff. That there’s a reflection API, however undocumented and likely to change, is a good sign.
