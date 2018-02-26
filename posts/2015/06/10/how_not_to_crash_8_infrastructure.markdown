@title How Not to Crash #8: Infrastructure
@pubDate 2015-06-10 15:13:00 -0700
@modDate 2015-06-10 15:13:00 -0700
Even if you think your app is crash-free, you need to collect crash logs — because there’s no such thing as crash-free: it can only be free of *known* crashing bugs.

There are a few different services for this, and the ones I’ve tried are pretty good, so I’m not going to make a specific recommendation.

But there are a few things it should do:

1. Crash logs should be collected without a user having to find them and send them to you. It should be automatic-ish (users should probably be prompted, if on OS X; on iOS nobody seems to expect a prompt).

2. There should be a way to group crash logs, and you should get a total for each group, so you know which ones are frequent and which aren’t.

3. You should be able to mark a group as resolved.

It’s not enough, of course, just to collect crash logs. You should look at them regularly. (I look at crash logs every morning.)

#### Bug tracker

Have one.

For my personal projects I use a combination of Lighthouse, OmniOutliner, and pen-and-paper — but you should use whatever works for you, as long as your crashes get into your bug tracker and don’t get lost.

(Lighthouse is a good bug tracker. For mapping out big new features or entire apps I like OmniOutliner, where I can build a tree of things-to-do. For short-term things — for the 10 steps needed to complete a single task — I like pen and paper, since it’s tiring to rely on short-term memory, since pen and paper doesn’t disturb the on-screen context.)

#### Errors and warnings

Xcode by default doesn’t turn on enough errors and warnings. I strongly recommend <a href="http://boredzo.org/blog/archives/2009-11-07/warnings">Peter Hosey’s set</a>.

The point is to remove *doubt* from your code.

I go a step further, which I also recommend: I turn on treat warnings as errors. This means that, yes, I can’t even debug locally if there’s a warning — but the discipline is worth it. It means that whenever my app is actually running, there are not even any warnings.

#### Instruments

Instruments is wonderful. It’s a very good idea to check how much memory your app allocates, and it’s super-important to check for leaks.

And if you’re getting crashes, it’s a good idea to use the Zombies tool. Your problem might not be related to zombies, but, when in doubt, it’s worth ruling out.
