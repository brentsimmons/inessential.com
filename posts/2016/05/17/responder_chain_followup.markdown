@title Responder Chain Followup
@pubDate 2016-05-17 13:27:10 -0700
@modDate 2016-05-17 13:28:39 -0700
<a href="https://twitter.com/jckarter/status/731991024206123008">Joe Groff reminded me</a> that checking for protocol conformance is Swift’s `respondsToSelector` equivalent:

<code>protocol RespondsToCopy { func copy() }</code><br />
<code>if let copier = responder as? RespondsToCopy {</code><br />
<code>&nbsp;&nbsp;return copier.copy()</code><br />
<code>}</code>

And, later, <a href="https://twitter.com/oscherler/status/732564801763872768">Ölbaum asked</a>:

>Wow, so all this fuss around lack of performSelector in Swift is just about laziness to use protocols?

My terse — and jerky, because it was the morning — answer was “No.” This post is the longer answer that the questioner deserves.

#### Let’s Do This Thing with This Thing

Take it from the top.

You’re in IB wiring up a menu item or button to First Responder. You set the selector as `copy:` — or, better yet, because I think people may get confused by using a common command, let’s say the selector is `goFishing:`.

To make this work with protocols instead of `respondsToSelector`, you then also type in a protocol name: `RespondsToGoFishing`. Or maybe the responder chain automatically generates that protocol name based on the selector. (Either way.)

In your code you define a `RespondsToGoFishing` protocol (as in the first line in Joe’s example above) and implement it in the various classes that can goFishing.

Then, after you’ve launched the app, you tap the button or choose the menu item. The responder chain walks its hierarchy, looking for the correct implementor.

What does the responder chain code have at this moment? Four things: a responder hierarchy, the sender (menu item, button, etc.), a reference to a protocol, and a selector.

(Let’s assume that some previous machinery turned the typed-in protocol name and selector from a string into more-usable types. Which assumes some kind of protocolFromString and selectorFromString methods, or some form of compilation.)

So the responder chain code looks something like this:

<code>if let actionImplementor = responder as? protocolReference.Self {</code><br />
<code>&nbsp;&nbsp;actionImplementor.&#8203;performSelector&#8203;(selector, withObject: sender)</code><br />
<code>}</code>

(I’m never sure if it’s Self or what. The above may not be strictly correct. But you get the idea.)

Conceptually this is not much different from the Objective-C version — the main difference is that it adds an entity (a protocol) which wasn’t previously needed. But I’m cool with that. (Maybe. It means adding a whole bunch of protocols — possibly one for every action method.)

For reference, here’s the Objective-C version:

<code>if ([responder respondsToSelector:selector]) {</code><br />
<code>&nbsp;&nbsp;[responder performSelector:selector withObject:sender];</code><br />
<code>}</code>

#### That’s fine, that totally works, but…

The point of my <a href="http://inessential.com/2016/05/15/a_hypothetical_responder_chain_written_i">previous article</a> was to imagine a responder chain written in Swift minus the Objective-C runtime.

So the above solution — with <code>actionImplementor.&#8203;performSelector&#8203;(selector, withObject: sender)</code> — won’t work in this hypothetical world, since `performSelector` is an Objective-C thing. And then there’s the need to convert from strings (protocol, selector) in IB to an actual protocol reference and a selector.

But — this is all just to say that perhaps it’s too early to be concerned with things like this, since we *do* have the Objective-C runtime (and AppKit and UIKit). At some point in the future, I imagine we’ll see Swift-minus-Objective-C-runtime app frameworks for Mac and iOS. And I will be very interested to see how these kinds of problems are solved.

I stand ready to be amazed, knowing it may be years from now.

In the meantime, though, it’s fun to write about.
