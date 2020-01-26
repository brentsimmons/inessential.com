@title Crash Math
@pubDate 2020-01-26 13:25:18 -0800
@modDate 2020-01-26 13:25:18 -0800
We’d like to ship NetNewsWire 5.0 for iOS in the first quarter of this year. The app is really close, but there are a [few bugs to fix](https://github.com/Ranchero-Software/NetNewsWire/milestone/4), including some crashes.

We’re sticklers about crashes: while there’s no way to guarantee the app will never crash — because there are bugs in other parts of the system that we can’t control — we want to get the number of crash reports as close to zero as we can. Ideally we’d go days or weeks between seeing a crash report.

This is about the craft of app-making. It’s about being responsible.

But it’s also about math. Consider this:

NetNewsWire for iOS could have 100,000 users. It’s relatively high-profile, in a popular category, and *free*.

So if we get it down to, say, a 1% chance that a given user will hit a crash on any given day, that sounds pretty good, right?

But that 1% chance means we’d get 1,000 crash reports per day. In other words, a 1% chance is *very, very bad*.

If we get it down to a 0.1% chance, we’d still get 100 crash reports per day. At that level, a given user could go, on average, 500 days between crashes. Which sounds great! Sounds like a super-stable app!

But that would mean 100 crash reports a day, which is still a *massive* number of crashes.

We need to do way better than that. (We will.)
