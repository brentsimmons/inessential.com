@title OmniFocus for Mac 2.2.5
@pubDate 2015-09-01 11:09:41 -0700
@modDate 2015-09-01 11:30:16 -0700
<a href="https://www.omnigroup.com/omnifocus">It just came out on the Omni site</a>, and will be on the Mac App Store once approved. It <a href="https://www.omnigroup.com/releasenotes/omnifocus-mac">fixes a couple crashes</a> — including one that I called The Last of the Big Crashes.

When I started working on OmniFocus last year, there was a set of the most common crashes and a set of crashes that were hit pretty rarely. So we fixed a bunch of crashing bugs — the most-common crashes and others — until we’re down to the rare crashes.

(If you read the <a href="https://www.omnigroup.com/releasenotes/omnifocus-mac">release notes</a> going <a href="https://www.omnigroup.com/releasenotes/omnifocus-mac/P5">back to 2.1</a>, you’ll see crash bug fixes in almost every release. Sometimes a bunch of them.)

I’ve often wondered if fixing crashing bugs leads to a more-successful app. It’s the right thing to do, regardless, so we do it. (In fact, I have to stop myself from being *too* obsessed with fixing crashes.)

But does that translate to more sales? Intuition tells me it does, since people using a trial version are less likely to hit a crash, and they’ll be more likely to buy the app. And people who have bought the app are less likely to hit a crash, and they’ll be happier with the app, and therefore more likely to tell friends, co-workers, and family about the app.

I would love to be able to tell developers unequivocally that fixing crashing bugs is good for the bottom line. But I can’t. I can only say it *maybe* helps — and then just appeal to our sense of professionalism. Fixing crashing bugs is the right thing to do. Period.

But, yeah, nobody tweets about how stable your app was today.

<p style="text-align:center">* * *</p>

The specific Last of the Big Crashes in 2.2.5 was this: an NSOutlineView had unsafe references to deallocated objects, and then calling `itemAtRow:` crashed. The solution was to make sure those objects would get deallocated afterward, not before, calling `itemAtRow:`.

(That sounds simple, but going from the crash logs to understanding the problem to figuring out the best way to fix it was anything but simple. There was even a period of an hour or two of staring at assembly code.)

(Of course we couldn’t reproduce it — not until we got some anonymized databases that people were kind enough to send in. We get *great* help from OmniFocus users.)
