@title Objective-Smalltalk
@pubDate 2014-03-12 13:32:07 -0700
@modDate 2014-03-12 13:36:30 -0700
I mentioned RubyMotion and Nu the other day, but missed [Objective-Smalltalk](http://objective.st/).

I like the syntax in that it gets rid of a bunch of brackets, braces, and parentheses. Lines of code look more like sentences — they even end with a period.

But I wonder if, in practice, I could get used to it. Some extra punctuation may actually help readability.

Check out the [Examples page](http://objective.st/Examples/). You see things like <code>self window makeKeyAndVisible.</code>

Is that easier to read than <code>[self.window makeKeyAndVisible];</code>? I’m not sure. It may be that, with practice, it’s at least *as* easy to read.

But: all that aside, what intrigues me most is that this is Smalltalk, and I’ve never written in Smalltalk, yet I’m aware that Objective-C is heavily influenced by it. It’s like Objective-C’s mom or dad.

Also: it has Higher Order Messaging.

<code>self view subviews do setNeedsDisplay</code> is way cooler than <code>[self.view.subviews makeObjectsPerformSelector:&#8203;@selector(setNeedsDisplay)]</code>.
