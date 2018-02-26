@title Vesper, Auto Layout, and Justin’s Book
@pubDate 2014-07-18 17:49:29 -0700
@modDate 2014-07-18 17:59:24 -0700
Last night I decided to use auto layout for some sub-sub-sub-view in Vesper for iPhone. Worked great. (I’m getting the hang of it.)

Except that it broke the interactive pan-back-from-detail transition. The view just wouldn’t move with your finger.

I have no idea why. I pulled out the little bit of auto layout code I was using.

So: enter Justin Williams. Today I emailed him to ask if his new book covered auto layout and interactive transitions, and he said he’d give it a shot.

I like how he’s doing this. He’s put out an <a href="http://carpeaqua.com/2014/07/15/achieving-zen-with-auto-layout-the-book/">early, unfinished version of his book</a> and he’s getting feedback as he goes. Very cool.

The thing I need to learn isn’t really using auto layout for layout — I’m getting the hang of that part. The Mac version is <em>all</em> auto layout, even. But the iPhone app barely uses it all, since the app is so full of animations and interactive transitions, and I just don’t get (yet) how to use auto layout with all this.

You might think I’d feel some urgency about auto layout, given the rumors of 4.7" and 5.5" iPhones. If the rumors are true, those screens might have different point dimensions than what we’ve seen so far. (Maybe. Even if they don’t, we should be prepared for it.)

However, it’s no harder to support different dimensions using layoutSubviews and layout code than it ever has been. There are a few places where Vesper hard-codes screen width at 320 points — but I could fix those in 15 minutes. The Credits screen is written to expect just two specific heights, but it wouldn’t take much work to make it work with variable heights (and it would probably simplify that particular code, actually). No other part of the app expects any particular screen height.

It’s not urgent, in other words, but it’s still important to switch to auto layout.

What’s cool about auto layout *isn’t* that it allows us to deal with different screens — we can do that the old-fashioned way just fine. All those Mac apps for all those years handled resizing windows and views without auto layout, after all.

What *is* cool is that we can switch from imperative to declarative style, and that matters. The more we can do of that with our UI code (which is so fiendishly boring to work on) the better.
