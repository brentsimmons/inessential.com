@title Swift Diary #11: Objective-Swift
@pubDate 2015-08-11 10:05:33 -0700
@modDate 2015-08-11 10:07:16 -0700
My main problems with Swift are:

* Collections of protocol-conforming objects don’t work as I need them to.

* No KVC.

* No equivalent of NSClassFromString.

Now, these aren’t really problems with Swift — they’re problems with *pure* Swift.

But there’s no such thing as a pure Swift app. The frameworks are Objective-C frameworks. You can’t load nibs without Objective-C.

Given that, I made the pragmatic decision to start using @objc protocols, classes, and collection types where those things make sense, where Swift fought against my design.

And suddenly the language is a joy to use. It’s like Objective-C but with type inference, no .h files, fewer imports, shorter syntax — *and* I get the things I was missing.

I’m still not sure I like optionals, and there’s more casting than I’d like, but overall it feels like Objective-C with less housekeeping. In this language — I’ll call it Objective-Swift — I can go *fast*.

<p style="text-align:center">* * *</p>

More about optionals…

For those who don’t know Objective-C: it’s based on message passing, and sending a message to a nil receiver is fine. It just doesn’t do anything. If it has a return type, it returns nil. (Roughly speaking.)

In other words: say <code>foo</code> is nil. The following in Objective-C is a-okay — nothing happens when foo is nil:

<code>[foo doSomething:someArgument];</code>

The Objective-C syntax is weird to everyone who isn’t used to it, I’ll grant. The above could be expressed in another language as <code>foo.doSomething(someArgument)</code>

What’s cool about this is that you can do nil-checking less often. Say you call a method that returns an object or returns nil. If it returns an object, you want to tell that object to do something, or you want to get one of its properties — or you want nothing to happen if the object is nil.

You can just skip the nil check and write your code as if the object isn’t nil.

I’ve relied on that behavior thousands of times. As an Objective-C developer it’s second nature.

There are obvious problems with that, though. One is that it’s not clear at all in the code that the object may be nil and nothing’s happening and it’s okay (it’s by design). Someone reading it — including future me — may not realize it, and it may be important.

The second, and related, problem is that nil as an *argument* rather than as a receiver is a completely different story. Plenty of methods will crash if you pass nil as an argument. So it’s not true that Objective-C code is free of nil-checking.

Along comes optionals in Swift, which make it clear when a thing may or may not be nil. When a variable is defined as optional, and you want to do something with it, you *have* to handle the nil case, and that’s enforced by the compiler.

That’s good — very good, in fact — except for all those times when I’m bugged because I have to satisfy the compiler when I feel like I shouldn’t have to, when years of experience tell me it’s quite okay to ignore the possibility of nil.

So I’m of two minds on optionals. Like many other things with Swift, I don’t really care about it for code that’s entirely mine — because I know my own style so well, because I know what mistakes I make and don’t make — but I *do* care about it for code that will have many authors.
