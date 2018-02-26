@title Reactive Followup
@pubDate 2016-04-10 12:12:31 -0700
@modDate 2016-04-10 12:21:12 -0700
Junior B. posted a good follow-up to his post that I had replied to previously. See [To React, Or Not To React](https://sideeffects.xyz/2016/to-react-or-not-to-react/).

Other followup…

#### On using other people’s code

<a href="https://twitter.com/b_gerstle/status/718765430135873537">Brian Gerstle asks</a>:

>@brentsimmons is it fair to say your only criticism of Reactive is that—in this case—its 3rd party code? If it was Apple, you'd use it?

I’m cautious with third-party code. I *do* use some: <a href="https://github.com/ccgus/fmdb">FMDB</a>, for example, appears in every app I’ve started from scratch in the last decade or so.

I like FMDB because the code is available (which is an obvious must-have); it’s relatively small; it does one job — providing an Objective-C wrapper for SQLite — and does it well; and it’s used in just one small section of my apps and has no impact otherwise.

Another example: recently I looked at at Fletcher Penney’s <a href="http://fletcherpenney.net/multimarkdown/">MultiMarkdown parser</a>, which I might use in an app I’m working on — and I like it for the same reasons I like FMDB.

I don’t have hard-and-fast rules about when to use other people’s code and when not to. But I’m most likely to say yes when the code is essentially a library that performs one conceptual function (database access, Markdown parsing, etc.).

I ask myself: what if something goes wrong and I can’t use Framework X anymore? Can I replace it somehow? Some amount of effort is fine, but rewriting and re-testing vast portions of the app is not acceptable.

I could write my own SQLite wrapper if I had to, and I could write my own Markdown parser. (Or find replacements written by other people.)

#### What if Apple made RxSwift?

Were Apple to provide reactive UIKit and AppKit and say, “Here’s how you make apps in the future,” I would expect that the tools would support this new style, and I’d expect it to play well with accessibility and AppleScript support and everything else. It would be well-integrated.

I’ve spent decades following Apple’s lead. People who don’t follow along end up in tight places — wishing for 64-bit Carbon, for instance.

That’s not say it *always* works out. Garbage collection, for example, was a dead-end (but with ARC it had a great replacement).

But, yes, I’d follow Apple’s lead into the reactive future in that case.

#### Not my only criticism

I wouldn’t be that happy about following Apple’s lead into the reactive future — if, that is, their implementation looked much like current versions.

So, no, not-being-Apple-code is not my only criticism. Another of my criticisms is that it’s difficult to read.

I’ve had a number of conversations with other developers on the subject, over many months, and almost every single developer that I talked to uses strong and inflammatory language about its unreadability.

If you’re a fan of this style, you might think that developers *shouldn’t* feel this way. My point is that, like it or not, they *do*.

You might not remember what it was like to look at this code before you understood it. Or you might be the kind of person who naturally takes to this particular style, and maybe it never seemed alien to you at all. Totally fine, of course, but remember that you’re not typical.

#### The revolution

I agree strongly with reactive proponents who say that the current standard ways of writing apps are broken. Too much state, for sure, and not enough ways to specify flow.

The less state we have to manage, and the more declarative code we can write, the better. I’m totally on board.

But if the revolution is about using this specific set of APIs, then I’m not on board.

My hope is that we’re using this specific set of APIs as a stepping-stone on the path to something better, something that appeals to a broader set of developers.

In the meantime, you could insist that there’s no readability issue, but I think that if you do then you’re potentially holding back the larger goal.

You could say, instead, “Yes, I know it sometimes looks like Perl in a blender. But we’re making the future here, and it doesn’t always start out pretty and it certainly doesn’t start out universally liked. This is step one. This is how we get from here to there.”

If so, then you’re taking one for the team, and I’m not — and I <em>thank</em> you.

PS Attribution note: the Perl-in-a-blender bit comes from <a href="https://twitter.com/pilky/status/717112523472904192">Martin Pilkington</a>:

>I’ve yet to see reactive code that didn’t look like Perl shoved in a blender, even though I like the idea in theory

PPS I may not have this story entirely right, but it went something like this: Picasso invents Cubism, and people think it’s ugly. Because it is. Then Braque, or Derain, or both (I forget) come along and do a prettier version. Picasso remarks that it takes a genius to do the first ugly version, and the people who make it nice don’t have to be geniuses.

(Or maybe it was Stravinsky, and it was some musical thing. Whatever. I like the honesty about the first genius version being ugly.)
