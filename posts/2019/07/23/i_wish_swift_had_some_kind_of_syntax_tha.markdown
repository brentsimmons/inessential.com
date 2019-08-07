@pubDate 2019-07-23 14:32:43 -0700
@modDate 2019-07-23 14:32:43 -0700
I wish Swift had some kind of syntax that declares that a function or property can used on the main thread only. If use is attempted from some other thread, then the app should crash.

I know I can — and already do — use a precondition and check that we’re on the main thread, but I keep feeling like this should be a language feature.
