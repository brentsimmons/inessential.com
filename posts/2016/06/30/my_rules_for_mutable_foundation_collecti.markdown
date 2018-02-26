@title My Rules for Mutable Foundation Collection Objects
@pubDate 2016-06-30 15:04:27 -0700
@modDate 2016-06-30 15:04:27 -0700
I have some simple rules that I always follow when dealing with mutable Foundation collection objects (plus mutable strings) in my Objective-C code.

#### Construction

I often use a mutable collection object when constructing a thing — array, dictionary, set, or string — and then pass it somewhere else.

Once it’s passed, ownership is relinquished. The construction code *never* continues to hold a reference to the thing it made.

Wherever that thing goes it’s treated as immutable (whether or not it really is).

#### No mutable collection objects in APIs

In my .h files, under no circumstances are properties or parameters allowed to be mutable  collection objects.

(Or, well, it’s *extremely* rare. There could be a utility API that takes a mutable thing, but that API does some kind of work that doesn’t retain that collection, so it can’t mutate it later on.)

#### Mutable collection objects are internal to a .m file

An object may use mutable collection objects internally, but those aren’t allowed to escape the .m file they live in. There’s no chance, then, that one of these could be mutated without its owner knowing about it.

<p style="text-align:center">* * *</p>

By following these rules — which, after all these years, I do without even having to think — I never run into an issue where I’ve passed a mutable array (or whatever) to another object, then held on that array and mutated it. It just can’t happen.

But, really, *whatever* — these days I write Swift code instead.
