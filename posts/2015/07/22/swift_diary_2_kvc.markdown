@title Swift Diary #2: KVC
@pubDate 2015-07-22 13:38:50 -0700
@modDate 2015-07-22 14:53:26 -0700
I was very glad to hear that performSelector and friends are supported in Swift in the latest Xcode 7 beta. But what I want to talk about today is a similar thing: [Key-Value Coding (KVC)](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/KeyValueCoding/Articles/KeyValueCoding.html).

I use KVC in a critical part of my apps: the part that creates model objects from database rows.

The database code is generalized and shared by multiple apps. I create a mapping (using a plist) that maps SQLite table names to property names and types.

The object creation code goes through the mapped property names and does the right thing for each name. In the end it boils down to something like this:

<code>[modelObject setValue:&#8203;someValueFromDatabase forKey:&#8203;propertyName];</code>

(This even works for non-object properties, which is brilliant on the part of KVC’s designers.)

I can do this in Swift, too. (Note that this is unchecked code, and I could have the syntax wrong.)

<code>modelObject.setValue&#8203;(someValueFromDatabase, forKey:propertyName)</code>

There are plenty of other places where KVC makes sense. (It’s part of a hearty, dynamic breakfast.)

Another example might be mapping NSTableView cells to values — a columns’s identifier might be configured to be the same as a property name, and so it’s easy to get the desired value:

<code>modelObject.valueForKey&#8203;(columnIdentifier)</code>

The coupling here is quite loose, and the compiler isn’t going to tell you if you’ve mistyped a property name. You’ve got all kinds of rope here.

But I’m totally comfortable with that. Here’s the deal I’m willing to make: to make my code more elegant (read: smaller, easier to maintain, reusable), I’m willing to let it crash if I’ve configured things incorrectly.

A bug here — say there’s a typo in a property name in my database mapping — will mean an instant crash, as the object has no such property name. I’m good with that. Crashes like that have zero chance of living beyond the time it takes me to build and run.

<p style="text-align:center">* * *</p>

If this is available in Swift, then why am I writing about it?

Because this is not a pure Swift thing: it’s a Swift + Objective-C thing. You can’t do this with structs, for example.

I want to get the advantages of structs. There are plenty of cases where my model objects could be structs. Structs are cool.

We’re in a transition period right now. Swift needs Objective-C so that people who rely on the dynamic nature of Objective-C — like me, like many developers — can write their apps.

It would be best, though, if Swift didn’t have to carry Objective-C baggage with it forever in order to make it adequate for the job of app-writing. I don’t think it *will*, even.

So my case is that Swift itself needs things like this. If not a clone of KVC, then something very much like it.

