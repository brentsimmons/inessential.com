@title Gocurious
@pubDate 2014-03-08 15:44:09 -0800
@modDate 2014-03-08 15:44:51 -0800
Over the years I’ve come to like subclassing less and less.

You can’t get away from subclassing NSObject, of course, and if you’re writing a view controller it has to subclass UIViewController. That’s how the frameworks work, and I don’t fight or even complain about this.

But in my own designs I’ve been stepping farther and farther away from subclassing. I like the flexibility, and the lessened brain-hurtiness, of protocols over subclasses.

Which brings me to a related topic: sometimes, at night, when I’m just reading random stuff on my iPad, I like to read about Go (golang). I haven’t used it for anything, but I find it fascinating.

(I’d most likely use it for server-side work, but it’s interesting to imagine as a client-side language.)

Here’s Rob Pike, one of the Go designers, in a [talk from June 2012](http://commandcenter.blogspot.de/2012/06/less-is-exponentially-more.html):

>My late friend Alain Fournier once told me that he considered the lowest form of academic work to be taxonomy. And you know what? Type hierarchies are just taxonomy. You need to decide what piece goes in what box, every type’s parent, whether A inherits from B or B from A. Is a sortable array an array that sorts or a sorter represented by an array? If you believe that types address all design issues you must make that decision.

>I believe that’s a preposterous way to think about programming. What matters isn’t the ancestor relations between things but what they can do for you.

>That, of course, is where interfaces come into Go. But they’re part of a bigger picture, the true Go philosophy.

>If C++ and Java are about type hierarchies and the taxonomy of types, Go is about composition.

One of the things I like about Cocoa is that it seems (am I right?) less subclass-happy than Java and C++. With protocols, the delegate pattern, and now blocks, we do tend to prefer composition over inheritance more than many object-oriented systems.

(But note that we still do subclass NSView, UIViewController, NSManagedObject, NSOperation, and so on.)

There are a bunch of other cool things about Go. It’s worth reading about, even if it only stretches your software developer’s muscles a little bit.

Another interesting article: [Go at Google: Language Design in the Service of Software Engineering](http://talks.golang.org/2012/splash.article), which is a text version of another Rob Pike talk from 2012:

>Type hierarchies result in brittle code. The hierarchy must be designed early, often as the first step of designing the program, and early decisions can be difficult to change once the program is written. As a consequence, the model encourages early overdesign as the programmer tries to predict every possible use the software might require, adding layers of type and abstraction just in case. This is upside down. The way pieces of a system interact should adapt as it grows, not be fixed at the dawn of time.
