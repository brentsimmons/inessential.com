@title objc-sweet-spot
@pubDate 2025-05-31 16:22:08 -0700

At work, for the last while, I’ve been leading an effort to get rid of our Objective-C code. When I started it was just shy of 24% of the app, and now it’s under 4%.

The reasons are the usual reasons: bugs, very much including crashing bugs, hide more easily in Objective-C code; the level of Objective-C expertise on this (and pretty much every) team diminishes constantly; and the need for Objective-C interop sometimes prevents us from using safer modern Swift features.

