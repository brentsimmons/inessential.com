@title High-Level Events
@pubDate 2016-04-12 13:47:24 -0700
@modDate 2016-04-12 13:52:17 -0700
I wrote, in <a href="http://inessential.com/2016/04/11/the_objective-c_version">The Objective-C Version</a>, that one of the major advances of Cocoa over the Macintosh Toolbox was event *routing*. Both frameworks were event-driven, but with Toolbox code you had to dispatch events manually to their proper places, while in Cocoa you hooked-up events and methods more directly. Which was genius.

But now we’ve been doing it the Cocoa way for years (and decades, for some people), and we take it for granted. We take it for granted so much that we’re now able to realize what a pain it can be. The thing Cocoa is missing — and what the reactive-programming folks get — is the notion of high-level events.

If events such as IBActions, NSNotifications, KVO-fires, timer-fires, delegate callbacks, and so on are primitive events, then a high-level event should be a composition of primitive events and conditions that don’t have to happen at the same instant.

#### Example

Consider again that live-search textfield from [Comparing Reactive and Traditional](http://inessential.com/2016/04/08/comparing_reactive_and_traditional).

There are two high-level events that could be described like this:

Textfield search event:

Primitive event: textField.stringValue changed<br />
Condition: textField.stringValue.count >= 3<br />
Condition: textField.stringValue unchanged for 0.3 seconds<br />
Action: runFetch(textField.stringValue)

Refresh button search event:

Primitive event: refresh button action method called<br />
Condition: textField.stringValue.count >= 3<br />
Action: runFetch(textField.stringValue)

I’m not saying we *want* to describe them using the syntax above — but it’s clear (from the above, and from RxSwift) that it is *possible* to specify high-level events.

It’s also clear (self-evident, I hope) that declaring high-level events means less code that synthesizes high-level events by querying and maintaining state (which is where your bugs come from).

(It’s also clear, I hope, that this is not all that RxSwift does. But it’s the part I’m interested in.)

#### How Apple might do it

It’s tempting to say that our synthesizing high-level events by breaking them down into small, logical pieces is why they pay us the big bucks. It’s what we’re trained to do, after all.

But that argument could be used against every single advance in app-writing, so let’s forget it.

Instead, let’s imagine how Apple might solve the problem.

Since high-level events are a UX thing, there would be some way in Interface Builder for your designers to specify high-level events. A drag-and-drop, point-and-click thing.

You’d wire up some triggering event (the primitive event), then create a predicate (the conditions), set some attributes (coalesced or not, coalesce interval), and then link it to an action method.

Because magic is disallowed, there would also be a way to do it in code. You could instead instantiate an NSHighLevelEvent object and set the trigger, conditions, and action.

You could write NSHighLevelEvent yourself — or HighLevelEvent, since it’s not Apple’s if you write it yourself — minus the editing interface in IB. To get an idea of its API, imagine something like this (quickly-typed thing) in your view controller:

<code>let textField&#8203;RunSearchEvent = HighLevelEvent&#8203;(observationTarget: self, key: "currentText")</code><br />
<code>textField&#8203;RunSearchEvent.&#8203;coalesced = true</code><br />
<code>textField&#8203;RunSearchEvent.&#8203;coalesceInterval = 0.3</code><br />
<code>textField&#8203;RunSearchEvent.&#8203;condition = NSPredicate&#8203;(…)</code><br />
<code>textField&#8203;RunSearchEvent.&#8203;target = self</code><br />
<code>textField&#8203;RunSearchEvent.&#8203;action = #selector&#8203;(runSearch(_:))</code>

What it means: when viewController.currentText changes (let’s assume HighLevelEvent always considers distinct changes), it coalesces changes for 0.3 seconds. Then it evaluates the predicate — and, if true, it then calls target.action(sender).

Obviously this is an object-oriented approach and is unlike reactive code. It has the benefit of fitting in better with the existing Apple frameworks (and the style of code most iOS and Mac developers have been using since OS X came out).

I do not suggest that this solves all the same problems RxSwift solves — but I do suggest that this approach would make app-writing a bit easier. You let the HighLevelEvent handle state (including setting up and tearing down a timer when needed).

Aside from setting up the HighLevelEvent, you’d have code that looks something like this in your view controller. Standard stuff:

<code>func textDidChange(textField: NSTextField) {</code><br />
<code>&nbsp;&nbsp;currentText = textField.stringValue</code><br />
<code>}</code>

<code>@IBAction func runSearch(sender: AnyObject) {</code><br />
<code>&nbsp;&nbsp;…</code><br />
<code>}</code>

In other words, this would fit in nicely with the way people write apps now, and would be something I’d use.
