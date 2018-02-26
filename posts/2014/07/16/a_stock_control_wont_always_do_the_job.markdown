@title A Stock Control Won’t Always Do the Job
@pubDate 2014-07-16 17:38:47 -0700
@modDate 2014-07-16 21:19:35 -0700
I wrote about <a href="http://inessential.com/2014/07/10/standard_controls">using stock and custom controls</a> the other day, and I was careful to make the point that sometime custom controls are absolutely needed.

<a href="http://vesperapp.co/appstore">Vesper</a> has a bunch of custom controls — far more than in any app I’ve made before. We could probably cut out a few of them, especially now that iOS 7 and 8 added features that we didn’t have when Vesper was first created, but we can’t cut all of them, or even half.

Here’s a small example:

If you’re a Vesper user, you know that tags sit above the keyboard when you’re editing. When you’re not editing, they appear below the end of the text.

The tags move as the keyboard appears and disappears.

You also know, if you’re a user, that tapping a tag gives you a little menu — much like the text editing menu — that lets you copy or remove a tag.

The tags themselves are a UIButton subclass. A fairly elaborate one, but still a UIButton.

That menu, though, is entirely custom. It’s not even a popover, since popovers won’t appear on iPhones until iOS 8. It’s a fake popover, custom from the ground up.

It seems like this is the perfect place to use UIMenuController. And, in fact, if you look at the menu (just tap on a tag to see it), you’ll see a black menu with white text, rounded edges, and an arrow pointing to the tag button.

It looks almost exactly like a UIMenuController menu, in other words. A normal, non-obsessed person wouldn’t notice the difference.

So why not switch to UIMenuController? Delete all that custom code. Great idea. (I love deleting code. Love love love.)

But UIMenuController wants the item attached to the menu — the tag button, in this case — to become first responder.

And, as soon as the button becomes first responder, the text view is no longer first responder, which means the keyboard falls away, and the tag buttons move so that they’re anchored at the end of the text. (And the UIMenuController menu shows and hides real quick, as if it’s been frightened by all the sudden activity.)

So we can’t use UIMenuController in this case.

We could do something entirely different — a UIActionSheet, for instance — but that would be a usability loss in this case. A UIMenuController-like-menu really is the best way to solve this problem.

Which means we have to use a custom control.

It’s possible that, in iOS 8, I could make it a real popover, but I’m not sure I’d have control I need over the appearance. (The corners have to be rounded just so, the arrow has to be the way it is, etc.)

Anyway. That’s show biz for ya.

<i>Update 9:15 pm</i>: Well, it’s possible to keep the keyboard up when using UIMenuController. See <a href="https://twitter.com/jaredsinclair/status/489623866323767296">Jared Sinclair’s tweet</a>.

I’m not sure that would actually work in my case, since it would hijack typing, which should go to the text view. (I say this without actually trying it, though.)
