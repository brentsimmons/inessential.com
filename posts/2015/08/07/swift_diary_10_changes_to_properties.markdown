@title Swift Diary #10: Changes to Properties
@pubDate 2015-08-07 16:47:50 -0700
@modDate 2015-08-07 16:47:50 -0700
Both of the apps I’m working on have a custom persistence engine (built on top of FMDB and SQLite). Core Data isn’t a great fit for these apps. (This isn’t me being contrary. I’m doing very database-y stuff, and Core Data is an object persistence system, not a database. Seriously: you should use Core Data.)

The model objects are pure Swift objects. And I’d like to borrow one of Core Data’s awesome features: when a property is set on an object, the persistence system should get notified. It will record the change, then coalesce and queue updates to the database.

<p style="text-align:center">* * *</p>

Let’s say I’m writing a Twitter client. (This an example used for historical reasons — because, if you look at history, you’ll find that people used to write Twitter clients — and should not be taken as indicative.)

Let’s pretend it has a Tweet class, a pure Swift class, with about 20 properties (some from the server, some local) — and setting any one of those should trigger the persistence system to do its thing.

I can do what I want if I add a <code>didSet</code> code block to each property. One of the cool things is that didSet is ignored during <code>init</code>, which means I can initialize an object with data without didSet getting called and triggering an unnecessary database update.

Each didSet block looks like a variation on this:

<code>recordPropertyChange(self, key: "somePropertyName", newValue: somePropertyName)</code>

It’s a pain to do this for every single property in every single class that’s database-backed.

<p style="text-align:center">* * *</p>

Were this Objective-C, the situation would be fairly easily dealt with via [dynamic method resolution](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/ObjCRuntimeGuide/Articles/ocrtDynamicResolution.html). Each property would be marked as <code>@dynamic</code>, and methods that do the right thing (update in-memory storage and notify the persistence system) would be provided at runtime.

That’s not available to pure Swift classes, though.

I could ask for that feature — but it had me thinking that there might be a better feature request to make. Classes could optionally (perhaps when conforming to a PropertyObserver protocol) implement a class method that gets notified when any property changes in the same circumstances where it would call didSet. (It should *still* call didSet, when it’s there.)

Something like:

<code>class func didSetProperty<T, U>(object: T, key: String, newValue: U) {</code><br />
<code>&nbsp;&nbsp;recordPropertyChange&#8203;(object, key: key, newValue: newValue)</code><br />
</code>}</code>

(I’m totally unsure that the above is the right way to express this. Maybe object should be Self? I’m still learning my way around generics and protocols.)

If there already *is* a way to solve this, and I don’t need to make this feature request, then I’m keen to hear the solution. It would be useful.
