@title NetNewsWire/Rainier Status
@pubDate 2019-05-07 13:40:13 -0700
@modDate 2019-05-07 13:40:13 -0700
The big thing remaining for [NetNewsWire](https://github.com/brentsimmons/NetNewsWire) 5.0 alpha is syncing with [Feedbin](https://feedbin.com/). My head is just not into syncing right now — I’ve done it too many times — but, luckily, [Maurice Parker](https://github.com/vincode-io) *is* into it, and he’s working on it right now, and making great progress.

#### NetNewsWire for Mac

There are some bugs to fix for 5.0 alpha — most of them small, but on that list is, of course, a new app icon. (Since an evergreen tree no longer fits the app.) There are some other cosmetic changes and very small features to consider too. But syncing is the big thing.

Once we get to alpha, then it’s all about testing, fixing any bugs that come up, writing the Help book, documenting the code, and getting the [website](https://ranchero.com/netnewswire/) closer to its shipping state (adding things like screenshots). A whole lot of writing, mainly — which I hope to get help with. Once that’s all done, then we’ll call it beta. (Beta is all about final testing and finishing the website.)

If things go well, we’ll hit 5.0a1 by WWDC. Fingers crossed!

#### NetNewsWire for iOS

The app is surprisingly far along (again, thanks to Maurice). It too is mainly waiting on syncing — but it also needs polish and UI review before it gets to alpha. My plan is to get there some time in the summer.

I expect to finish it after finishing the Mac version. I’m not trying for a simultaneous release. (Why bother? It’s harder to do a simultaneous release. It’s better to ship what’s ready to ship the moment it’s ready.)

#### Rainier

While Maurice is working on syncing, I’m taking a NetNewsWire break and working on [Ballard](https://github.com/brentsimmons/Ballard), the language built-in to [Rainier](https://github.com/brentsimmons/Rainier). Currently working on the parser and evaluator (the thing that runs scripts).

I’ve never written a language before, and I’ve always wanted to. It’s fun! And brain-bending. (I’m writing all of it by hand. In Swift, of course.)

One of the goals with the language is to create something simple but easy-to-learn and useful. How-it-works should be understandable to anyone who wants to peek under the hood. (Since it’s open source, you can learn the entire thing.)

The language, and much of Rainier, will also be embedded into NetNewsWire — because that will allow me to use it to write new features for the app *and* it will allow people to automate NetNewsWire using an easy scripting language with a built-in storage system. (Other apps could embed it too. Even yours.)

My two apps are not just related — I think of them as two parts of the same project. Something about the open web and the [freedom](http://inessential.com/2019/04/23/freedom) and power to make things.

#### Rainier for iOS

There could be a Rainier for iPad some day. I’m not sure it would make sense as an iPhone app — but as an iPad app, definitely. (Though I’m not sure Apple would approve it. If not, you could build it on your own.)

It’s even possible — depending on what we see at WWDC — that I could write the UI using UIKit and Marzipan. I totally will, if that still means I can make a great Mac app *and* deliver it outside of the App Store *and* not have to sandbox it.

We’ll know soon enough!

But, for now, I’m still working on the lower levels of Rainier, which would be shared code regardless (the language, standard library, storage system, etc.).

Anyway. That’s where I’m at. :)

PS There’s a single Slack group for both NetNewsWire and Rainier. Email me at brent@ranchero.com if you’d like an invitation.
