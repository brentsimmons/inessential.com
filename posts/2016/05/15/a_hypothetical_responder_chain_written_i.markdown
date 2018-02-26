@title A Hypothetical Responder Chain Written in Swift
@pubDate 2016-05-15 11:35:19 -0700
@modDate 2016-05-15 12:01:14 -0700
My piece <a href="http://inessential.com/2016/05/14/the_tension_of_swift">The Tension of Swift</a> started out as a piece talking specifically about the Responder Chain and how you might write it in Swift. It got almost entirely rewritten before being published.

I was thinking specifically of commands like Copy, where a menu item or whatever has an action selector `copy:` but no target — which means the framework travels the Responder Chain until it finds a responder that implements `copy:`, and then calls it.

(Note: it could be any selector at all — `goFishing:`, for example — but the Copy command makes a good example.)

A simplified version of the framework’s implementation looks like this. Given the first responder, a sender (the menu item or button or whatever), and a selector:

	while(responder != nil) {
		if ([responder respondsToSelector:selector]) {
			[responder performSelector:selector withObject:sender];
			break;
		}
		responder = responder.nextResponder;
	}

So I tried to come up with a Swift version — a Swift-minus-the-Objective-C-runtime version — and I came up with this (from my unpublished first draft):

>You’d have each object in the Responder Chain conform to a protocol with two methods:

>`func respondsToCommand(command: String) -> Bool`<br />
>`func performCommand(command: String)`

>Then, in your menu items (and buttons and wherever), you’d set a command string like “copy” and “goFishing” and so on.
​
>The Responder Chain would then walk its hierarchy and ask each object if it `respondsToCommand`, and when it returns true, if would call its `performCommand` method with the command string.

​You might slice this up differently than I did — you might very well make it more Swift-like — but in the end I think you’d still end up passing strings and doing `switch` statements based on an action string.

The Swift version *is definitely safer*, though the Objective-C version was effectively safe, because you’d have to go out of your way to make it fail, and you’d find out pretty quickly. (Though, yes, at runtime.)

The Swift version also adds more housekeeping. The Objective-C version requires you to implement a copy or goFishing method, but no more than that. A major part of the beauty of AppKit and UIKit is *not* having to do the kind of housekeeping that other app frameworks require. (We start out on the 20th floor of the building.)

There’s also an aesthetic argument to make. Objective-C’s message-passing is a perfect fit for this exact kind of problem. In my Swift version I’ve recreated a simplified message-passing, but not as a feature of the language, as more of a thing bolted-on in order to solve a problem that really wants to be solved by message-passing. This is, I think, undeniably less elegant than the Objective-C version.

<p style="text-align:center">* * *</p>

I feel like I have to say it every time: I’m writing all my new code, both at work and on personal projects, in Swift, and I enjoy it, and I don’t want to write Objective-C any more.

And: I appreciate Swift’s type safety — I’m even <a href="https://twitter.com/brentsimmons/status/730510539344863232">learning to love optionals</a>. But the thing I keep coming back to is that great app frameworks require languages with dynamic features. And, as an app writer, I’m less concerned with the language than with the frameworks.

Objective-C the language was always a bit of a odd duck, though lovable — and it allowed these truly magnificent frameworks to be built, and using those frameworks has been one of the joys of my career.

I want the app frameworks of the future to be just as wonderful. More so.

<p style="text-align:center">* * *</p>

PS Also see Daniel Jalkut’s <a href="http://indiestack.com/2016/05/brents-swift-tension/">optimistic take</a>, Manton Reece on <a href="http://www.manton.org/2016/05/apples-mindset-on-swift-dynamic-features.html">Apple’s mindset on Swift dynamic features</a>, and Rob Fahrni on <a href="http://iam.fahrni.me/2016/05/09/a-swift-only-future/">A Swift Only Future?</a>.

Rob writes:

>This is the beginning of the radical departure from Cocoa I’m hoping for. A day when all Framework code for building Mac and iOS applications is void of Objective-C, or mostly void of it. Not that Objective-C and Cocoa are bad, they’re not. It’s just time to move on…

>Will there be pain? Absolutely. Is it possible to overcome it? Of course it is. It will take a lot of work and planning for companies to move to Swift and Framework X, but it will take years for Apple to get there, so we all have quite a bit of time.

<p style="text-align:center">* * *</p>

*Update 12:00 pm*: I keep wanting to find a way to express my nervousness succinctly. I think it’s this: there’s a difference between a language that makes writing high-quality code easy and a language that makes writing high-quality *apps* easy.
