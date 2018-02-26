@title More Notes on Vesper
@pubDate 2016-08-21 15:56:17 -0700
@modDate 2016-08-21 16:06:01 -0700
This is the first time I’ve ever shut down an app. In the past I’ve sold my apps (MarsEdit, TapLynx, Glassboard, NetNewsWire) — and two of those are still going. (I’m writing this post — like all my posts — in MarsEdit.)

<p style="text-align:center">* * *</p>

We never debated about providing an Export feature — not only was it the obvious right thing to do, it was a feature we’d planned to do regardless.

Initially I thought we’d do it as a web app. You’d kick off an export, then the web app would create a zip file and send you email later so you could download it.

We didn’t do it this way because it sounded like a real pain to write, and, more importantly, it didn’t do anything for people who didn’t use syncing.

The iOS document provider feature — which was introduced after Vesper shipped (it was originally an iOS 6 app) — was just what we needed. It meant we could write the notes and pictures as files in a folder, and then a document provider could upload those files to iCloud Drive, Dropbox, or wherever.

Perfect. It works whether you’re syncing or not — it has nothing to do with syncing.

And it will continue to work even after sync shuts down. It will continue to work as long as you have the app on your device.

<p style="text-align:center">* * *</p>

We decided to make it so that new users can’t sign up for syncing, since it’s going away. And, since a new user can’t sync, we can’t really ask them to pay for the app, either — so we made it free.

Consider the alternative: we allow new sync users, and we continue to charge for the app. Some people would buy it the same day we shut down syncing. That’s not good.

Since it’s free, it will probably get more downloads in the next few weeks than it’s had in its entire life.

<p style="text-align:center">* * *</p>

Some people have asked that we make it open source. The request is getting serious consideration, but I can’t make any promises.

The code is all Objective-C. It’s an iOS 6 app with just enough changes to keep it working on iOS 7 and beyond. It knows nothing about size classes, presentation controllers, and so on. Doesn’t even use auto layout. It’s *not* an example of how you’d write an app these days.

<p style="text-align:center">* * *</p>

Belief inside Q Branch: if we had started with a Mac app rather than an iOS app, Vesper would have been much more successful. That wasn’t clear at the time we started, though (Dec. 2012).

<p style="text-align:center">* * *</p>

This is the last app on the App Store where I wrote all (or almost all) of the code. Odds are excellent that there will never be another app written largely by me on any app store.

(Yes, my day-job-apps are on the app stores, but they’re written by a team.)

I’m working on new stuff from Ranchero Software. I had planned two apps, but I think it’s going to be just one, just because two takes too much time. So I picked the one I’m more passionate about.

It’s a Mac app, because I’m a Mac developer at heart, and it won’t be on the Mac App Store because I prefer the freedom of shipping instantly, without any large corporation’s bureaucracy slowing things down and holding veto power.

And then that will be my app. The thing I work on for the next 10 or so years, until I retire. That’s the plan. (To be clear, though, I don’t plan to leave my day job, which I love.)

When will it ship? I don’t have a date. I don’t know.
