@title Benefits of NetNewsWire’s Threading Model
@pubDate 2021-03-21 17:39:50 -0700
@modDate 2021-03-21 17:39:50 -0700
In my previous post I describe [how NetNewsWire handles threading](https://inessential.com/2021/03/20/how_netnewswire_handles_threading), and I touch on some of the benefits — but I want to be more explicit about them.

#### It Reduces Bugs and Makes the App Stable

I would not be surprised, were it possible to know, that the largest trigger for bugs and crashing bugs (among iOS and Mac apps) is threading issues of various kinds.

Our threading model eliminates this category.

We have zero known threading bugs or crashes in production, and they’re extremely rare in development. When they appear in development they’re due to a mistake in following the model. (Something like forgetting to dispatch to the main queue when calling a callback, for instance.) They’re quickly and easily fixed.

#### It Makes the App Faster and More Efficient

The app does not suffer from thread explosion, which is bad for performance. Ever stop your app in the debugger and notice that it has dozens of threads? Or maybe notice that in a crash log? Not an issue for NetNewsWire.

But, more importantly, we don’t hide performance and efficiency issues by moving work to a background queue. Instead, we use the profiler in Instruments to figure out what’s slow, and then we fix it. Only after doing that would we consider moving work to a background queue.

#### It Saves Developer Time

Things NetNewsWire developers don’t have to do:

* Diagnose and fix threading bugs and crashes — which are often excruciating-to-impossible to reproduce and difficult to fix
* Think about how to do background work (there’s a simple model for how to do it)
* Figure out how to protect shared mutable state

This gives us more time — which is super-valuable in an open-source, all-volunteer project — to do work that improves the lives of the people who use the app.

It also improves the experience of our developers, who can concentrate on the feature they’re working on instead of on how the feature can live safely in a multithreaded universe.

Best of all: nobody is spending time tracking down a maddening threading bug that never happens on their machine, and then implementing a speculative fix — only to find later that it’s *not* the fix but now, actually, there’s a new crashing bug, which might have been triggered by that “fix”… and so on, forever.

Developer morale is important!
