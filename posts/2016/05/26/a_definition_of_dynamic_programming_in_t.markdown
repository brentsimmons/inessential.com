@title A Definition of Dynamic Programming in the Cocoa World
@pubDate 2016-05-26 13:19:47 -0700
@modDate 2016-05-26 13:20:40 -0700
When I talk about dynamic programming on iOS and Mac, I mean this:

1. An app can learn about its structure at runtime.

2. An app can do things based on what it knows about its structure.

3. An app can make changes to its structure.

The first is things like knowing what methods an instance implements, or getting a reference to a protocol, class, or method from a string. (As in NSSelectorFromString and so on.)

The second is things like being able to instantiate a class where the name wasn’t known at compile time, or to call a method or reference a property that wasn’t known at compile time. (As with `performSelector:`, KVC, the responder chain, and xib and storyboard loading.)

The third is things like adding methods at runtime (a la Core Data) or adding classes — for instance, by loading compiled code from disk (plugins).

(Note — because people sometimes misread what I write — this definition is not advocacy for a particular style of programming, nor is it a judgment of Swift, which, I repeat, I love, and is my preferred language. It’s to help us know what we’re talking about when we talk about dynamic programming.)
