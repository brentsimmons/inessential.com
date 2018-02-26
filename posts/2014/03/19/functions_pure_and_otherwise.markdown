@title Functions Pure and Otherwise
@pubDate 2014-03-19 13:45:19 -0700
@modDate 2014-03-19 13:57:27 -0700
I don’t hate writing code in C. Quite the opposite — I love writing in C. It’s low-level enough to be fun. (Languages are fun when they’re either very low level or very high level.)

From time to time I wonder how much of the typical app could be written in C. Often I’m not thinking of C-and-only-C: I’m thinking of C functions but allowing Cocoa types.

That is, the app would be mostly C functions, but you’d still use NSArrays and everything else you’re used to when using Foundation and UIKit/AppKit objects.

There’s nothing you could do about some situations: you have to subclass NSView, UIViewController, and similar. The frameworks just don’t work otherwise.

But there are so many things that don’t actually have to be Objective-C objects.

Looking at Vesper: database access could all be in C (making heavy use of blocks and GCD). Thumbnail renderer and thumbnail cache — C. Attachments storage. [VSTheme](https://github.com/quartermaster/DB5). Much of the sync system. Parsers. Etc. These could all be implemented with C functions (but allowed to use Cocoa objects).

Not that I’m doing that.

But here’s what tugs at me about it — my parents taught me a basic rule: a function should take some arguments and then return something based on those arguments. It should always return the same thing, given the same input values, and it shouldn’t look at anything else but those arguments.

I was raised on [pure functions](http://en.wikipedia.org/wiki/Pure_function), in other words.

Pure functions are not only conceptually beautiful, they’re also easy to think about and they’re especially valuable when dealing with concurrency.

Not that everything listed above would be entirely pure — database and file system access doesn’t make for pure functions. But rendering a thumbnail does. Transforming JSON into a model object does. Merging two model objects does.

So there’s another thing that tugs at me — a certain type of honesty. There are all these singular resources, things that will only ever exist once and once only: the database of notes, the folder of attachments on disk, and so on. Pretending that these are object-oriented doesn’t feel quite right.

#### C APIs

I’m a fan of well-done C APIs. But when designing these you run into a dilemma pretty quickly, and that dilemma illustrates the tension between pure functions and singular resources.

Do you:

1. Create static variables inside the .c file? Or…

2. Pass around a pointer to a struct that the functions take as an argument?

If you do the first, your functions won’t all be pure because they refer to internal state.

But if you do the second you’re making coding more difficult — you have this pointer to pass around. Every caller needs to have a reference. And maybe you’re pretending that a thing could have multiple instances when really there’s just the one, which is not strictly honest. (But also isn’t the worst thing.)

#### Inventing Object-Oriented Programming

Consider Objective-C. It’s exactly as if you’re implicitly passing around a pointer to a struct to every method, and the pointer is always called self.

*This is nice.* It sort-of solves the dilemma with C APIs described above.

But it leads me to wonder if the following (contrived example) is a pure function or not:

<code>- (NSUInteger)numberOfNotes {</code><br />
<code>&nbsp;&nbsp;return [self.notes count];</code><br />
<code>}</code>

That’s a pure function if you remember that self is the implicit first argument. It’s not mutating anything or doing I/O. Given the same inputs it will return the same value every time.

But I don’t think of it as a pure function. It is arguably referring to state outside of itself (even though, arguably, it’s not).

Given that I make my [Mom](https://twitter.com/maggiejdavis) happy when I use pure functions, I’m tempted to write it like this:

<code>- (NSUInteger)numberOfNotes:(NSArray \*)notes {</code><br />
<code>&nbsp;&nbsp;return [notes count];</code><br />
<code>}</code>

But that’s absurd — it’s more work, and numberOfNotes is only ever about the number of notes in self.notes. It begs the question of when the parameter might be something other than self.notes. (And all I’ve done is push work to the caller, which has to reference self.notes.)

It’s absurd, but I still understand wanting to do it. I tend not to, but I often kind of wonder if I *should*, since I really really (as is obvious by now) like pure functions.

This is where I get a little frustrated with object-oriented programming. If you agree with me that the first version of numberOfNotes is not pure, then I think you have to say that object-oriented programming works against pure functions.

It also works against the honesty of presenting single things as single things, since the system is designed for multiple instances.

(C isn’t necessarily better: instead, those two things, purity and singleness, can work against each other.)

#### Sympathy

I end up thinking more and more about [functional programming](http://en.wikipedia.org/wiki/Functional_programming). I haven’t done any — but it’s so close to my earliest coding lessons that it talks to the lowest, most basic layers of my programmer’s brain.

I listen to a small voice that is strict about no side effects and no mutations and no looking outside the parameters list, and that voice is constantly complaining about object-oriented programming.

Which makes me highly sympathetic to the goals of [ReactiveCocoa](https://github.com/ReactiveCocoa/ReactiveCocoa), while at the same time I wonder if functional programming is too much standing-on-your-head for user interface code, which is all about state. (I draw no conclusion: I’m just wondering, and I’m keen to find out the answer.)

It also makes me interested in languages such as [Go](http://golang.org/) and [Rust](http://www.rust-lang.org/). And so on.

Anyway. Things are happening.
