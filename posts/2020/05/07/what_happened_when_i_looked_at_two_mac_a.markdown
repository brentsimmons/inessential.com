@title What Happened When I Looked at Two Mac Apps Today
@pubDate 2020-05-07 15:40:59 -0700
@modDate 2020-05-07 15:40:59 -0700
I’m not going to name names here. Don’t worry. :)

I’m in the market for a Mac app for _____. It’s a not-uncommon need, and so I figured I’d have some good choices.

I’d also like an iOS app that syncs with that Mac app — but the Mac app is the more important of the two, because I sit in front of a Mac all day. (To me. Some people are iOS-first, which is totally cool.)

I downloaded and tried a couple apps. One required an account just to try the app, which pissed me off, but I did it anyway.

#### Window Resizing Test

The first thing I tried, with each app, was to resize the window. This is a good test because I get frustrated with sluggish apps: window resizing is a decent way to get some idea of how the app performs.

I know I’m not playing fair — I’m on a 2013 MacBook Air — but the app I write is fast on this machine, and other apps should be too.

Both apps were sluggish with window resizing. They were bad enough that I could have just stopped right there.

But it was actually worse than that.

With one of the apps, the upper position of the window could actually *change* during window resizing. It could even go offscreen. I don’t even know how that bug is possible.

The other app was almost as bad: the upper position of the window would sometimes jump down around 20 pixels then back up, real fast. It made the window seem to flicker. Nasty.

The basics of window resizing behavior should be impossible to mess up — AppKit should be handling this. If it’s messed up, then something in the app is fighting the frameworks. That’s a bad sign for the quality of the rest of the app.

#### Undo Test

I picked an action that would be 1) super-common and 2) something that every user should expect to be undo-able.

In one app, I did the thing and then chose Undo. It didn’t do anything that I could see — the Undo command was available, but had no visible effect. I did Undo again. No visible change. God knows what was happening.

In the other app, Undo just wasn’t available. This is actually better than a faulty Undo — but, still, it’s not good.

#### That Was Pretty Much It

I poked around a little more, enough to find some additional bugs, and then I trashed both apps. I deleted the account I had had to create for the one app.

By not paying attention to the basics of a good Mac app, each of these apps lost a potential customer who’s 1) happy to financially support app development, and 2) who has a blog that a bunch of people in our community read, where he likes to praise things that are good.

Maybe that’s not worth it? But doing a not-good Mac app *is* somehow worth it? I don’t understand.
