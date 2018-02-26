@title Beware of _flags
@pubDate 2015-03-03 11:27:48 -0800
@modDate 2015-03-04 10:32:19 -0800
If you’ve done AppKit programming, you’ve noticed in header files (such as NSTableView.h) that Apple sometimes uses a _flags struct to hold a bunch of booleans.

Something like this:

<code>typedef struct \_\_flags {</code><br />
<code>&nbsp;&nbsp;unsigned int a:1;</code><br />
<code>&nbsp;&nbsp;unsigned int b:1;</code><br />
<code>&nbsp;&nbsp;unsigned int c:1;</code><br />
<code>} \_flags;</code>

(Usually there are more than three. Usually way more, at least in Apple’s code.)

A BOOL is one byte — <code>sizeof(BOOL)</code> returns 1. So, in theory, you could store a bunch of these 1-bit things in the space normally reserved for a single BOOL.

But what actually is the size of \_flags? In the case above, where it has just three members, it’s four bytes — <code>sizeof(_flags)</code> returns 4. (On my 64-bit Mac, that is. I haven’t checked everywhere, but I wouldn’t be surprised if this case is always 4 on Apple platforms.)

This means that declaring those three members as BOOL properties would have saved space. If there were four members you’d break even — but the _flags version is more complex.

I think, in fact, that’s there’s only good case for a _flags struct: when you have way more than three booleans, and you expect to have a ton of these objects in memory at once. (A table view, for instance, wouldn’t count.)

Otherwise, do the easy, less-complex thing: stick with properties.

<i>Update Mar 4 10:30 am</i>: Well, there was a big thing I missed. If you make those unsigned char instead of unsigned int, you can in fact pack a bunch of booleans into a byte.

<code>typedef struct \_\_flags {</code><br />
<code>&nbsp;&nbsp;unsigned char a:1;</code><br />
<code>&nbsp;&nbsp;unsigned char b:1;</code><br />
<code>&nbsp;&nbsp;unsigned char c:1;</code><br />
<code>} \_flags;</code>

<code>sizeof(_flags)</code> returns 1 in this case.

Nevertheless, I still maintain that it’s rarely a good idea. Mostly because it adds complexity (you have to support KVC and KVO manually) but also partly because in framework code (for frameworks that aren’t compiled when the app is compiled) it’s fragile.
