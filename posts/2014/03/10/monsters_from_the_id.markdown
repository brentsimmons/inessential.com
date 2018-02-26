@title Monsters from the id
@pubDate 2014-03-10 20:24:31 -0700
@modDate 2014-03-10 20:30:13 -0700
[Marcel Weiher reminds](http://blog.metaobject.com/2014/03/cargo-cult-typing-or-objective-c.html) us that `id` is the default type, and that it’s perfectly legal to write code like this:

<code>-objectAtIndex:(NSUInteger)anIndex</code><br />
<code>{</code><br />
<code>&nbsp;&nbsp;if ( anIndex < [self count] ) {</code><br />
<code>&nbsp;&nbsp;&nbsp;&nbsp;return objects[anIndex];</code><br />
<code>&nbsp;&nbsp;}</code><br />
<code>&nbsp;&nbsp;return nil;</code><br />
<code>}</code>

Marcel also writes:

>There is a subset of the language, which I’d like to call the *id subset*, where all the arguments and returns are object pointers, and for this it was always safe to not have additional type information, to the point where the compiler didn’t actually have that additional type information…

>What’s great about the *id subset* is that it makes incremental, explorative programming very easy and lots of fun, much like other dynamic languages such as Smalltalk, Python or Ruby.
