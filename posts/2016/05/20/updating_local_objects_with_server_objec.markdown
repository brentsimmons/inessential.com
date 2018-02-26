@title Updating Local Objects with Server Objects
@pubDate 2016-05-20 13:43:26 -0700
@modDate 2016-05-20 14:02:09 -0700
I’ve spent much of my career writing apps that store objects locally that come from the web — and that may *change* on the web, and then need to be updated locally.

This kind of code can be tedious to write. Given a local object and an objectified version of some JSON or XML or whatever, I’d write something like this (translated to Swift for fun):

<code>if localObject.foo != serverObject.foo {</code><br />
<code>&nbsp;&nbsp;localObject.foo = serverObject.foo</code><br />
<code>&nbsp;&nbsp;changeDictionary[fooKey] = serverObject.foo</code><br />
<code>}</code><br />
<code>if localObject.bar != serverObject.bar {</code><br />
<code>&nbsp;&nbsp;localObject.foo = serverObject.bar</code><br />
<code>&nbsp;&nbsp;changeDictionary[barKey] = serverObject.bar</code><br />
<code>}</code><br />
<code>// multiply above a dozen times and for several different classes</code><br />
<code>return changeDictionary</code>

Maybe you spotted the bug in the above, and maybe you didn’t — and that’s part of my point. I’d write this code using copy-and-paste, and then go over it visually, line-by-line, to make sure it’s right, and sometimes I’d miss something anyway.

If `foo` and `bar` are both strings, for instance, the above would compile and all would be well. Except that I’ve written a bug where <code>localObject.foo = serverObject.bar</code>.

Eventually I found a better way — some code that I can write once, and that can’t have the bug I wrote above. <a href="https://gist.github.com/brentsimmons/47fa9c49cf4efb8e024541d651b6ebd2">See this gist</a>.

<p style="text-align:center">* * *</p>

The solution is pretty simple. You have two objects — which may or may not be the same class but where the properties have the same names — and then loop through an array of mergeable property names. (The two objects don’t have to have the exact same list of property names. They just have to have the mergeable property names and types in common, since those are the ones we care about.)

Then there’s a method that compares the local and server objects. For each property name in the list, it gets the localValue and serverValue using `valueForKey:`, and then compares them (via `isEqual:`).

When they’re not equal, then it uses `setValue:forKey:` on localObject to give it the serverValue. It also adds the property name and new value to a change dictionary. (That dictionary could be useful for efficient database updating, sending notifications, etc.)

There are places this could go wrong, and where the compiler wouldn’t complain. In the gist there’s this line:

<code>static let mergeablePropertyNames = ["dog", "cat", "zebra", "numberOfAnimals", "fedTheTigers", "attendingDoctors"]</code>

Obviously that line has to be maintained, and it has to be true that both local and server objects have those properties and those properties have to be of the same type. Yes.

However, you’re going to notice any error at runtime pretty quickly, since you’ll get an exception — while you may not notice the `localObject.foo = serverObject.bar` bug from the manual version any time soon.

Best thing: you can reuse that <code>updateLocalObject&#8203;WithServerObject</code> method for all the various local/server object updating you need to do in all your apps.

<p style="text-align:center">* * *</p>

Even though we’re writing in Swift here, the solution uses the Objective-C runtime and <a href="https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/KeyValueCoding/Articles/KeyValueCoding.html">KVC</a>.

KVC is both awesome and to be used *sparingly*. Most of the time you want to write standard code that the compiler can better check — you want to write `foo.bar = true`. Absolutely.

But there are those occasional critical cases where KVC creates more reliable code that’s easier to maintain, debug, and reuse. This is one of those.
