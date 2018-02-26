@title Comparing Reactive and Traditional
@pubDate 2016-04-08 10:44:52 -0700
@modDate 2016-04-08 11:41:05 -0700
My friends <a href="https://twitter.com/jamiepinkham">Jamie Pinkham</a> and <a href="https://twitter.com/caseyliss">Casey Liss</a> wrote a short sample meant to illustrate the kind of code you’d write in RxSwift to implement a text field that runs a search via the web and then updates a table view.

The rules:

* Changes to the search text must be coalesced over a period of 0.3 seconds.

* When the search text changes, and the text has four or more characters, an http call is made, and the previous http call (if there is one) must be canceled.

* When the http call returns, the table is updated.

* And: there’s also a Refresh button that triggers an http call right away.

Basic live search text field, in other words, with just the added wrinkle of a Refresh button.

Because I thought it would be fair to compare to a traditional version, I wrote one. Both samples — theirs and mine — surely have errors, and neither compiles. They’re for the sake of discussion rather than meant as actual, running code.

Here they are:

<a href="https://gist.github.com/cliss/51cb740b14f3cd56ba1d11f2a9a6ba02">Reactive version</a> by Jamie and Casey<br />
<a href="https://gist.github.com/brentsimmons/387c5ec75aa1a5373d929fd9f1ae5f43">Traditional version</a> by me

#### Status Quo

The traditional version is, in general shape, the same code you’d have written 15 years ago. We have blocks and Swift and ARC now, and so it’s smaller and simpler — and more readable and maintainable — than it used to be. But the main idea is the same. And we’re all just plain tired of writing code like this.

The two biggest knocks against it:

1. Dealing with mutable state sucks. Every time you add something it gets more complex. “State” is a fancy name for “where bugs live.”

2. There’s no high-level view of what’s actually happening, unless it’s in a comment. It’s a collection of small functions and properties without a linear story.

It’s not all bad, though. It sticks close to the frameworks and the language, and so any Cocoa developer can understand it, even the newest member of your team. The properties and functions are named reasonably well, and they’re small and logical. It’s the least clever thing you can imagine that still does the job.

#### New Coolness

The <a href="https://gist.github.com/cliss/51cb740b14f3cd56ba1d11f2a9a6ba02"">reactive version</a> has the advantages that the traditional version lacks:

1. There is far less state to manage directly.

2. There is a linear description of what happens — it reads almost like a paragraph.

These are *huge* advantages. Giant.

It’s not all good, though. To the uninitiated, it looks like write-only code, which means the newest member of your team faces a learning curve. It also means there’s a large dependency on a third-party framework.

#### The trade-offs

As a (very) hypothetical CTO, I’d nix any dependency that great, and especially one that comes with that much learning curve. But that’s just me — another person might say the trade-offs are worth it. (See those awesome advantages again.)

My experience tells me to avoid cleverness and stick as closely as possible to what Apple provides — “don’t fight the frameworks” is old and still-good advice. This is not just for the sake of new members to the team but also for the sake of the future, so that you can debug and extend the code in one year or five years or ten without rewriting it. It also means that as the frameworks evolve you can take advantage of those changes with the least amount of trouble.

Another worry is illustrated by the use of `throttle(0.3)` in the reactive version. I seriously doubt that it’s polling <code>textField.&#8203;stringValue</code> every 0.3 seconds — but you have to look, because you’re responsible for the quality of your app, which means you have to know implementation details about the framework.

#### But!

But doesn’t the traditional version just plain *suck*?

Damn right it does, and, even though it’s gotten easier to write these things, it’s been just matters of degree. We’ve been writing this stuff that same way for a long time, and it’s still bug-prone and tedious, and I don’t want to do it any more than you do.

I think the future is declarative, and the Reactive solution is closer to that in many ways — it tells the story of the flow. But one problem with it is that it’s not that readable. The traditional version is, in some ways, more readable.

#### What I really want

I want to be able to write something like this:

* runFetch with textField.stringValue when textField.stringValue changes and its character count is 4 or greater, with changes coalesced by 0.3 seconds.

* runFetch withTextField.stringValue when the Refresh button is tapped.

But if I look at the above, it looks kind-of like AppleScript. And that means it will fake you out — it *looks* like English, but in reality it would be strict and weird and hard-to-write. So I don’t *really* want to write faux-English code.

I think I want something more like this:

<code>runFetch with textField.stringValue when {</code><br />
<code>&nbsp;&nbsp;textField.stringValue changes {</code><br />
<code>&nbsp;&nbsp;&nbsp;&nbsp;distinctly</code><br />
<code>&nbsp;&nbsp;&nbsp;&nbsp;coalescedBy(0.3)</code><br />
<code>&nbsp;&nbsp;&nbsp;&nbsp;count >= 4</code><br />
<code>&nbsp;&nbsp;}</code><br />
<code>&nbsp;&nbsp;or button "Refresh" tapped</code><br />
<code>}</code><br />


That’s not Swift, or anything else, of course.

#### Change

Part of me does not want to encourage people to use RxSwift for the reasons I’ve outlined. But part of me very much <em>wants</em> to encourage people to use RxSwift — because change comes, in part, from the community pushing the state of the art.

(Example: were it not for all the enthusiasm for functional programming in recent years, Swift might not have `filter` and `map` functions.)

Luckily, you’re not going to listen to me either way.

If you don’t use RxSwift, I totally don’t blame you. We’re in the same boat.

But if you do use it, and some time in the future there’s a nice, declarative way of handling events and dealing with state, then I’ll have you to thank for helping make that come true.

PS Jamie wrote an <a href="https://bitbucket.org/notjessepinkman/brent_rx_sample">entire working example that uses RxSwift</a>. Definitely check it out. (Huge thanks go to Jamie and Casey for all their work here. Top-notch humans.)
