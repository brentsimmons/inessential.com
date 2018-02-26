@title Frontier Diary #3: Built-in Verbs Configuration
@pubDate 2017-04-13 22:25:41 -0700
@modDate 2017-04-25 13:39:20 -0700
Frontier’s standard library is known as its built-in verbs. There are a number of different tables: `file`, `clock`, `xml`, and so on. Each contains a number of verbs: `file.readWholeFile`, `clock.now`, and so on.

Most of these verbs are implemented in C, in the kernel, rather than as scripts. At the moment, to add one of these kernel verbs, you have to jump through a few hoops: edit a resource, add an integer ID, add to a switch statement, etc. It’s a pain and is error-prone.

So I want to re-do this in Swift, because I’m all about Swift. And I want adding verbs to be fool-proof: I don’t want to remember how to configure this every single time I add a verb. Adding a verb needs to be *easy*.

My thinking:

* Give each table its own class: ClockVerbs, FileVerbs, etc.
* Have each class report the names of the verbs it supports. These need to be strings, because we get a string at runtime.
* Run a verb simply by looking up the selector, performing it, and returning the result.

To make things easy and obvious, I think it should work like this: the selector for a given verb is its name plus a parameter. Then there’s not even a lookup step.

Each verb will take a VerbParameters object and return a VerbResult object.

	dynamic func readWholeFile(_ params: VerbParameters) -> VerbResult

The flow goes like this:

1. We have the string `file.readWholeFile`.
2. We see the `file` suffix and so we know we need a `FileVerbs` object.
3. We check `fileVerbs.supportedVerbs` (an array) to see if `readWholeFile` is in the list. It is.
4. We construct a selector using the `readWholeFile` part of the string and we add a `:` character: `NSSelectorFromString(verbName + ":")`

This is great! We’re almost home free. Then we run the verb:

	if let result = perform(selector, with: params) as? VerbResult {
		return result
	}

That doesn’t work. We get:

	Cast from 'Unmanaged<AnyObject>! to unrelated type 'VerbResult' always fails

Nuts.

<p style="text-align:center">* * *</p>

It was *so* close.

In Objective-C this would have worked. And obviously, apparently, I still think in Objective-C.

I investigated some other options. At one point enums were abused, because there’s *always*, in Swift, an enum-abuse step. But everything I tried was more code and was more error-prone, and my goal here is to improve the situation.

I think, in the end, I’m going to do something that looks kind of ugly: a switch statement where the cases are string literals.

	switch(verbName) {
	case "readWholeFile":
		return readWholeFile(params)
	…
	}

“Nooooo!” you cry. I hear ya.

My experience as an object-oriented programmer tells me this: if I write a `switch` statement, I blew it.

And my experience as a programmer tells me that string literals are a bad idea.

But the above may actually be the easiest to configure and maintain. Each string literal appears only in that one switch statement and nowhere else in the code. And the mapping between a verb name and its function couldn’t be more clear — it’s right there.

(Yes, instead of using a string literal, I could create a String enum and switch on that. But that’s actually more code and more room for error. I’m going to have to type those string literals *somewhere*, so why not right where they’re used?)

It does mean that `readWholeFile` appears three times in the code (the string literal, the call, and the function itself), and in an Objective-C version it would appear only twice (in a `supportedVerbs` array and the method itself).

But. Well.

I’m torn between shuddering in abject and complete horror at this solution and thinking, “Hey, that’s pretty straightforward. Anybody could read it. Anybody could edit it.” Which was the plan all along.

And I get to stick with Swift, so there’s that.

But, sure as shootin’, some day someone’s going to come across this code and say, “Brent, dude, are ya *new*?” And I’ll send them the link to this page.

<p style="text-align:center">* * *</p>

<i>Update the next day:</i> well, the `performSelector` thing *would* work, if only I’d known about Swift Unmanaged objects.

<a href="https://twitter.com/jckarter">Joe Groff</a> told me how this works.

Here’s the gist: the `Unmanaged<AnyObject>` just needs to be unwrapped by calling `takeRetainedValue` or `takeUnretainedValue`. Once unwrapped, it can be cast to `VerbResult`.

All this means that I can use my original design, which is great news.

<p style="text-align:center">* * *</p>

<i>Update April 25, 2017:</i> I ended up using enums after all. See <a href="https://github.com/brentsimmons/Frontier/blob/master/FrontierVerbs/FrontierVerbs/VerbTables/MathVerbs.swift">MathVerbs.swift</a> for an example.
