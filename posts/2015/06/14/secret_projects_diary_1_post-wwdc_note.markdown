@title Secret Projects Diary #1: Post-WWDC Notes
@pubDate 2015-06-14 13:37:19 -0700
@modDate 2015-06-14 13:37:19 -0700
Note: This series — which will probably last a long time — is my attempt at writing about things without actually announcing what they are. I’ve decided I can eat this cake and still have it.

The point is *not* to tease — though I realize that that’s a side effect, and I apologize in advance. (It’s not going to stop me from saving actual announcements until the software is ready, and it’s not going to stop me from writing in the meantime. Because writing helps me think, and it’s fun.)

#### Swift

I started working on my apps a few months ago, and there was no question at the time that I should use Objective-C. But now with Swift 2 I wonder if it’s time to switch.

The new Swift goes a long way toward curing <a href="http://inessential.com/2015/02/04/random_swift_things">angle-bracket blindness</a>. But, more importantly, now we know what Swift will be once it grows up (and it’s growing up fast) — and that thing, a protocol-centered language, is a thing I want.

(The most important session of this year’s WWDC was <a href="https://developer.apple.com/videos/wwdc/2015/?id=408">Protocol-Oriented Programming in Swift</a>. It’s a peek into how we’re going to be writing software for the next decade and more. For the rest of my career.)

I haven’t written much UI code yet. Almost everything so far has been data transformations — isolatable things that run outside the main thread, things that could benefit from Swift structs and enums rather than the collection of classes that I’m currently using.

Objective-C is a living language, but Swift is the safer bet for the long term. And I want my apps to last a very long time.

I’m torn between wanting to make forward progress and wanting to port the code so far. I haven’t decided yet. I might do these things concurrently.

#### OS X 10.11 and Auto Layout

My apps will both require 10.11. That was never in doubt.

One of the interesting changes is that AppKit (with split views, particularly) has more of a concept of a sidebars and content lists. And there are some new behaviors, such as automatically hiding a sidebar and showing it as an overlay, that we get if adopt the new APIs.

At least one of my apps (and possibly both; undecided for now) will have a sidebar. But I wasn’t planning on using Auto Layout because I’ve had problems with performance, bugs (in NSToolbar), debugging, and with actually getting things to work the way I want. (I have not been able to replicate Mail’s splitview handling using NSSplitViewController, for example, but I can replicate it if I go the old-fashioned route.)

Auto Layout solves a problem I don’t have. I’ve been writing manual layout code for so long that I barely even have to think about it. It’s easy. While I understand the benefits of declaring (as opposed to coding) layout, those benefits disappear when things go wrong and when I can’t do the thing I want to do.

But this leads to a dilemma. Doing things the old-fashioned way means manually writing sidebars-that-overlay (and so on) *and* nailing the behavior perfectly *and* revising it every time the behavior changes. If I use Auto Layout instead, I get the behavior, and any changes to that behavior — but I also get an unknown set (of unknown size) of struggles and frustrations.

If it’s a tie, then the winner is the future-proof answer. Which is Auto Layout.

#### NSStackView

Stack views in 10.10 are slow. (I can point to multiple performance issues in shipping apps that are a result of stack views.) Word on the street is that they’re much-improved in 10.11 — which is great. If that’s true, then I want to use them.

There are lots of cases where a stack view is the best answer to a layout problem, and so I suspect there will be plenty of stack views in my apps. (As long as they truly are faster now. I haven’t checked yet.)

#### http deprecation

This one worries me a little, and I need to find out more. Since neither of my apps will be sandboxed, it may not be an issue.

But it’s a larger issue in the industry and is bound to have an impact on what I do sooner or later.

What upsets me about this issue in general is that it’s anti-democratic: it can make writing for the web more expensive and difficult for individuals. As a writer, reader, and open web partisan I dislike everything that shifts power away from people and toward entities with greater resources. What you end up with is corporate speech rather than the voices we know and love and need to hear.

This is a complex situation, though. I strongly believe in the right to privacy, and that encryption should be used much more widely than it is today, and that no organizations, official or otherwise, should have back doors.

Well. Anyway. More research and thought required on this one.
