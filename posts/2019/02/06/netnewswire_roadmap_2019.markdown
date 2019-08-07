@title NetNewsWire Roadmap 2019
@pubDate 2019-02-06 18:05:46 -0800
@modDate 2019-02-06 18:05:46 -0800
Let’s look back at last year first.

#### 2018: Evergreen to NetNewsWire

As 2018 started, the app was called Evergreen, which I still think is a pretty great name for an RSS reader. I’d been working on it for about four years, on weekends and at nights.

It was usable-by-me a year ago, and a few other people were using it, even though it was missing all kinds of important features.

And then, some time in the spring of 2018, I thought to contact the folks at [Black Pixel](https://blackpixel.com/) about getting NetNewsWire back. Seemed like a total longshot. But why not try?

And they surprised me by being interested! In fact, they mentioned that they’d already been talking about it.

I was clear that I wanted just the name — not the code, not the then-current users, not the sync service. The app named Evergreen would be renamed as NetNewsWire, but would be, in every other way, the same app I was going to write. It would still be free and open source.

They agreed. And then, of course, discussions, mostly internal to Black Pixel, happened for a few months, because that’s how these things go — and we managed to make it official on August 31, 2018. (See [NetNewsWire Comes Home](http://inessential.com/2018/08/31/netnewswire_comes_home).) Black Pixel gave it to me for free (we never haggled over price; that was their plan all along), and their generosity remains one of the things I’m most thankful for in my entire career.

Soon after that I renamed Evergreen to NetNewsWire — and memorialized the name Evergreen in the app’s bundle id: `com.ranchero.NetNewsWire-Evergreen`. (NetNewsWire will always be Evergreen.)

And so it turned out that I had been working on NetNewsWire 5.0 for four years already! I just didn’t know it for most of that time. :)

The rest of the year saw more work on the app, with code contributions from [Maurice Parker](https://github.com/vincode-io), [Olof Hellman](https://github.com/olofhellman), and [Daniel Jalkut](https://github.com/danielpunkass), with bug reports on GitHub, with the help of the folks on the NetNewsWire Slack group. (Which you can join too: just email me.)

That was 2018.

#### 2019: Let’s Ship This Thing

At this writing we’re down to [seven bugs in the 5.0 Alpha milestone](https://github.com/brentsimmons/NetNewsWire/milestone/1). There are three main things: syncing with Feedbin, searching, and the app icon.

I want to ship 5.0 by WWDC, which is (most likely) the first full week of June. So here’s what I’m planning:

* Finish those last bugs, and ship 5.0a1.
* During the alpha period: write the Help book and document at least some of the code. *Test*, most importantly. Fix any bugs that get reported. Once there are no known defects, after a suitable period of testing, then ship 5.0b1.
* During the beta period, continue testing. The code will be touched only with great reluctance. (Every beta is a shipping candidate.) Continue documenting the code.
* Once there are no known defects, ship 5.0.

As you can see, the 5.0 Alpha milestone represents five years of work, and the alpha and beta periods ought to be relatively short, possibly just a couple weeks each.

But how quickly we get to alpha is mainly a function of how quickly I can get Feedbin syncing working and bug-free.

I *think* I can get it done by WWDC, but I could be wrong! No promises, of course. For NetNewsWire, app quality is everything, and hitting a date means very little.

#### Beyond 5.0: More Sync

There’s every chance that WWDC will bring changes and new technology from Apple that I’ll have to deal with. That’s expected — every app developer (hopefully) budgets for this. Assuming 5.0 is out before WWDC, then I can deal with this stuff in an update in the summer, in time for the next macOS.

There’s a huge list of features I could work on after that — there’s so much room for growth — but I think the big one has to be adding support for more syncing systems. I’m likely to do Feedly next, since it appears to the the most popular.

So my hope is to get Feedly support shipping by the end of 2019. And, if I do, then it will have been a very good year.
