@title On Alternate App Icons for NetNewsWire for iOS
@pubDate 2020-03-13 19:50:39 -0700
@modDate 2020-03-13 19:56:43 -0700
Releasing an app always comes with surprises. No matter how many beta testers you have, there’s nothing like an app actually going out to the public.

We’ve had, for [NetNewsWire](https://ranchero.com/netnewswire/) for iOS, a startling number of requests for the ability to choose from a list of alternate app icons.

This is a thing that some people really like these days. Even if it’s the exact same icon just with different color treatments. (A dark icon seems to be most commonly wished-for.)

This was *not* a thing the last time I released an iOS app. ([Vesper](https://github.com/brentsimmons/Vesper), back in 2013.) My guess is that, in the intervening years, we got API for this, and some developers have done this because, well, it’s fun. 🍕

And now it’s a thing people expect.

Given that including additional app icons can’t slow down the app, why not just do it? What could possibly be the downsides?

#### Here Are All the Downsides

The first one is kind of obvious. It’s easy to think that this is something you could do in a couple hours. But remember that it’s not just a case of loading the app icon up in Photoshop and doing some quick versions with different colors.

The colors have to be chosen and tested. Each version has to be created in all the various different sizes. It’s quite a bit of work!

And our app icon maker [Brad Ellis](https://twitter.com/bradellis) is a father. Like everyone else on the team, he’s donating his time. Do I ask him to spend a few nights on this?

A second downside is that this takes time away from fixing bugs and doing things like bringing Feedly syncing to the Mac. (This feature requires layout, code, and testing — it’s not just Photoshop work.)

The third downside is that each option we add takes NetNewsWire one step further away from the *simple* RSS reader that people love. We will have to add options in the future — but, knowing that, we need to be super-careful about what we add so it doesn’t balloon. (You probably don’t remember NetNewsWire 3.3.2’s preferences window. It was *extensive*.)

The fourth downside is related to the third, and might be the most important. My previous decade of experience with NetNewsWire tells me that there is a sizable set of users who get kind of stuck on things like this. The more customization there is, the more time they spend on it. Any time we add something like this, we’re adding to their anxiety.

To be clear: I’m not disdainful of these people, not in the least tiny bit. I recognize it in myself, even. I want the ability to make things just-so, and it never, ever is, quite, but I keep trying. And maybe I ask the developer to add just one more option, but with this particular shade of blue or orange — and they do, but it’s still not quite right, so I go back to tweaking some more, maybe going another route… and…

This just isn’t good.

#### What We’re Doing

These are still very early days for the app — and so we’re going with a couple simple policies.

<b>Add options when needed for accessibility.</b> We support Dark Mode, for instance, which is for many people an accessibility issue. (We use Apple’s colors for this, on the grounds that they’ve done more research and design for this than we ever could.)

<b>Add options that reduce anxiety.</b> An example of this is the option to not show the unread count in the Dock on Macs. (There’s a similar setting in Notifications settings in iOS.)

Alternate app icons won’t help with accessibility, and they certainly won’t help with anxiety.

That’s not to say we wouldn’t ever do this. Or we might just add a dark version. But not right now.

I know this will disappoint some people. My pledge is that, even when I’m disappointing you, I will tell you honestly why.

(We’ll probably do themes for the article view way before we would do something like this, because 1) that’s fun too!, and 2) it’s an accessibility/readability issue.)
