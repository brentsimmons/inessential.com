@title On Vesper and Working Efficiently
@pubDate 2014-08-04 13:46:12 -0700
@modDate 2014-08-04 14:29:42 -0700
The great thing about the Cocoa frameworks is that we get a ton for free, so we can spend our time working on what’s special and different in our apps.

But, of course, that’s only true when we actually <em>use</em> those features. If we spend our time making <a href="http://inessential.com/2014/07/10/standard_controls">from-scratch custom controls instead of standard controls</a> — for instance — then our apps are more expensive to create than they need to be, and it’s harder to make a profit.

In <a href="http://www.marco.org/2014/07/28/app-rot">App Rot</a>, Marco goes beyond just the issue of custom vs. standard controls and says:

>Efficiency is key. And efficiency means doing more (or all) of the work yourself, writing a lot less custom code and UI, dropping support for older OSes, and providing less customer support.

>Apple is greatly helping our efficiency. Every version of iOS brings new capabilities that make previously difficult features much easier. iOS 7’s redesign gave indie developers a huge advantage by making the stock UI cool again.

So true. I’m constantly thinking about ways to work more efficiently.

But, because we’re talking about software development, once you get to the concrete level of an actual app, it’s full of hard choices and dilemmas. I’ll talk about some of these choices we have to make as we work on Vesper.

#### The Problem of Fonts

Vesper has a ton of custom UI. Alerts, various popover-like things, the sidebar, swipe-to-reveal table cell buttons, and so on. Things that look like navigation bars are custom. Even the search bar handling — which stays pinned to the top of the screen instead of scrolling with the table — has a bunch of custom code, though the search bar itself is (almost) standard.

Some (not all) of these custom things exist *only* because we want to use Vesper’s font instead of the system font. (This isn’t unique to us. Plenty of iPhone apps use embedded fonts. <a href="https://overcast.fm">Overcast</a> is a recent example.)

Though we need to work efficiently, <em>design still matters</em>, and Vesper is designed around typography. We’re not even going to think for one second about dropping the embedded font.

But that leads to this dilemma: do we switch to the standard controls that don’t let us use our font, or do we stick with our custom controls?

If we stick with the custom controls, then we have more code to maintain, and, to a certain extent, we have to track Apple’s changes with each iOS release.

If we switch to standard controls, how do we justify the cost of switching? It may lead to less code and an easier-to-maintain app — but it’s <em>more work right now</em>, and doing that work doesn’t fix any bugs or add more features. And then we have that situation we didn’t want, where Vesper’s font and the system font compete with each other.

It reminds me of pre-Yosemite OS X, which distinguished between system and user fonts, and both were sans-serif. It was weird. But at least on OS X that was an established thing, where on iOS it’s most definitely not. And clearly the direction of UI design is to use just one font, not two.

(Yes, I could hack into the view hierarchy in some cases and change the font. But that’s bad engineering and I don’t like it. Vesper does it in exactly one place, so that the Cancel button next to the search bar uses our font.)

#### View Controller Transitions

Vesper was written during the iOS 6 days. The main screens use view controller containment, but the transitions were written before iOS 7 introduced standard ways of doing custom transitions.

iOS 8 is coming, and we’re still using iOS 6 code. Should I revise this code to use the new features in iOS 7 and 8?

That might not actually simplify things, but it’s been my experience that you don’t want to get too far behind on things like this. And there’s always the possibility that another coder could help with the app some day — and they’d be less at sea if they saw what they expect to see rather than my custom transitions system.

But it’s more work to make the change, and, again, it’s work that doesn’t actually fix any bugs or add new features.

Nevertheless, you’d have to call this technical debt, and technical debt should, in general, be dealt with.

But it’s not clear to me yet that we could actually accomplish replacing Vesper’s current transitions with the new system. And I’d hate to do all that work only to find out it’s not do-able. That would be an incredibly inefficient use of my time.

I actually don’t know know what to do. The default — doing nothing — may be the best call.

#### Swipe-to-Reveal Table Cell Buttons

iOS 8 lets us customize the buttons that appear when you pan a table cell to the left. This is great.

Since we can’t customize the font, we’re not sure we can use this. But the pull toward looking and feeling like a modern iOS app is very strong.

And it gets a little worse: Vesper lets you swipe a note to archive it, without having to stop and tap an Archive button. This isn’t supported by the new UITableViewRowAction  feature. We’d have to take away the archive-in-one-motion feature — which would be a shame. It’s an integral part of Vesper.

And then it gets just a little bit worse still: Mail on iOS 8 *does* have the ability to keep swiping to get the default action. Mail must be doing this as a custom thing or using private APIs to get this.

Which means that if we adopted the standard behavior, people would ask us why we don’t “just” do what Mail does.

Which argues for not touching this at all, since we already do a custom thing which works.

But that, again, means we’ve got this custom code to maintain and a bit of UI that’s quite unlike what users expect. (Which isn’t necessarily the worst thing. There can be good reasons for doing something different.)

#### Lessons

You can learn a few things from my experience.

One is that doing an app with an embedded font is expensive, far more expensive than just the cost of licensing the font. If you’re willing to accept Clash of the Fonts — your font is used everywhere except in system-generated UI — it’s not so expensive. But if your app is at the place on the design curve where an embedded font is a good idea, then it’s probably at the place where you wouldn’t accept that conflict.

Another is that working efficiently from the start is a good idea. You want to avoid the situation where you’ve done custom work and are now faced with either going standard or revising your custom work — because *both* options require work. If you’d started with standard stuff you’d have less work to do. But there are also the cases where you created something custom that becomes a new standard part of iOS in a later release, and the dilemma is unavoidable.

A last lesson is that you can’t avoid doing <em>some</em> work. Even standard controls and features get deprecated and replaced, and you need to think hard about when and how to deal with iOS changes — and iOS changes come every single year. Can you give up every summer, every year, to getting your apps ready for the next version of iOS? You might have to, no matter what you do.
