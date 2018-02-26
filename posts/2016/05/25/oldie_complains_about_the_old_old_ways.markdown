@title Oldie Complains About the Old Old Ways
@pubDate 2016-05-25 13:52:42 -0700
@modDate 2016-05-25 15:02:55 -0700
I saw a thing on Twitter that said I’m just an old guy complaining about the new ways. Then the tweet was deleted, to the credit of its author. But let me take up the point.

It’s not the *new* ways that bother me — it’s the old *old* ways. That is, how I wrote apps before I started using AppKit.

In those days it was common to use C or C++ — always C for me, thankfully — and you may or may not have used an app framework (MacApp, PowerPlant, MFC, etc.). The app framework might generate code for you, which was a source of fragility and bugs. But, even if not, you had to do things like this:

Menu item with unique ID is chosen<br />
App’s central event handler is called<br />
App looks at its context and dispatches event to the right function

There were *lots* of switch statements. To add, for instance, a copy (or whatever) implementation to a particular view, you’d have to edit your event dispatcher to know about that particular view and its copy function. Making changes required making changes in various places.

Sure, there were things you could to make this a bit easier. It didn’t have to be total spaghetti. But, even at best, it was bad code, and there was nothing you could do about it.

Contrast that with the first time I used AppKit about 15 years ago. I wrote an action method in a view, wired it to a menu item in Interface Builder, *and it worked*. No switch statements, no touching a half-dozen locations just to add a command.

I’m sure, that first time, that I didn’t even wire that menu item up to First Responder. It was wired directly. But, even still, AppKit used the runtime’s dynamic features to be able to find and call the right object and the right method. And that’s still true today. (Even in UIKit. Even if it’s a button. In other words, if you don’t think you’re taking advantage of Objective-C’s dynamic features, you totally are.)

It seemed like magic, then. I later came to understand how it worked, and then it just seemed like brilliance. (Brilliance is better than magic, because you get to learn it.)

<p style="text-align:center">* * *</p>

So when people like me write about these problems, it’s not because we fear the future and new ways of doing things. We love learning new ways of doing things — particularly when they’re better solutions to the problems we have.

We’re not afraid of the future — we’re afraid of the *past*.

We remember how these problems were solved by the static languages of the day, and we don’t want to go back. In the <a href="https://twitter.com/gte/status/735370823507312640">words of Guy English</a>:

>If you see a switch statement or dispatch table they blew it.

So, again, I’m documenting the problems currently solved by Objective-C’s dynamism, and suggesting that Swift, as it evolves, needs to take these problems into account. The foundation should be built with some idea of what the upper floors will look like.

The answer doesn’t have to be that Swift is dynamic in the way Objective-C is, or even dynamic at all. But the eventual Swift app frameworks need to solve these problems as well as — hopefully better than — UIKit and AppKit do right now. And those solutions start with the language.

PS I think I’ll write about plugins next.
