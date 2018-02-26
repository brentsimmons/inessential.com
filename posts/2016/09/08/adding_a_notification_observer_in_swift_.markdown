@title Adding a Notification Observer in Swift Using a Name Defined in Objective-C
@pubDate 2016-09-08 09:38:28 -0700
@modDate 2016-09-08 09:38:28 -0700
I spent hours on this. This post exists for anybody Googling this particular problem.

Here’s the issue: I have a mixed Objective-C and Swift app.

I have a Swift class that needs to observe a Notification (aka NSNotification) posted in Objective-C code. The notification name is defined in a .h and .m file:

.h:

<code>extern NSString *SomethingHappenedNotification;</code>

.m:

<code>NSString *SomethingHappenedNotification = @"SomethingHappenedNotification";</code>

In Swift I tried a number of permutations, trying to get the notification name correct, including using <code>Notification.Name&#8203;(rawValue: SomethingHappenedNotification)</code> and similar. Each try resulted in a compile error.

The answer came from Tim Ekl (privately) and <a href="https://twitter.com/UINT_MIN/status/773918317924880384">Jordan Rose (on Twitter)</a> independently at the same time:

>Ah, the word "Notification" is stripped from the name as redundant, so it becomes Notification .Name.Some (or just .Some).

In other words, the syntax for adding an observer looks like this:

<code>NotificationCenter.default.addObserver(self, selector: #selector(someSelector(_:)), name: .SomethingHappened, object: nil)</code>

Note that the Objective-C name <code>SomethingHappenedNotification</code> becomes just <code>.SomethingHappened</code> in Swift, and it’s automatically a Notification.Name.

It seems obvious now! But it wasn’t (at least for me). So: if I saved you some time today, then go be nice to somebody. :)
