@title Prefixes Considered Passé
@pubDate 2014-07-24 11:28:47 -0700
@modDate 2014-07-24 11:53:07 -0700
<a href="https://twitter.com/brentsimmons/status/492373018056740864">Me on Twitter</a>:

>Decided. No longer prefixing classes in app code, even with Objective-C. I can hear your screams and I don’t care.

Prefixing was always a poor solution to the lack of namespaces in Objective-C. There was no enforcement anywhere — and a prefix like RS could stand for Ranchero Software, Red Shed, Red Sweater, and Rogue Sheep. (Those are all real companies that used RS.)

A couple things have made me decide not to use prefixes in app code class names anymore.

First is that I’m spoiled by Swift. I didn’t think it would make much difference to me to be able to use naked class names — CreditsViewController instead of VSCreditsViewController, for example — but it does. It’s much nicer.

The second is that the Xcode 6 betas no longer ask for a prefix when starting a new project. And it creates AppDelegate and friends — not BSAppDelegate and friends.

If I had to guess, I’d say that Apple engineers are also spoiled by Swift’s no-prefixing, and somewhere in developer tools a decision was made not to push prefixes for app code any more.

This — no prefixes for app code classes — will become a recommendation, I’d bet.

There is a caveat, though. There could be non-prefixed class names in Apple’s frameworks. I haven’t personally verified these, but <a href="https://twitter.com/ObjColumnist/status/492373468877697024">Spencer MacDonald says</a> there’s a `Message` class and <a href="https://twitter.com/casademora/status/492379024576880640">Saul Mora says</a> there’s a `BluetoothDevice` class. There could be more.

Avoiding these conflicts is the point of prefixing. We can argue that it’s the responsibility of frameworks to use prefixes so that we app developers don’t have to watch out for these — but arguing doesn’t make it so.

Nevertheless, I’d bet these are rare enough that it’s the worth the potential hassle, and we can always file Radars if these come up.
