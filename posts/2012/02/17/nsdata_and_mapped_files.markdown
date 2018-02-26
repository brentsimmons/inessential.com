@title NSData and Mapped Files and Cleanup
@pubDate Fri Feb 17 12:07:55 -0800 2012
@modDate Fri Feb 17 12:08:17 -0800 2012
Tom Harrington posted a clever (in a good way) solution to the problem of cleaning up an internal data structure used in a category in <a href="http://www.cimgf.com/2012/02/17/extending-nsdata-and-not-overriding-dealloc/">Extending NSData and (not) Overriding dealloc</a>.

>Really what I’d like to do is wrap the code above into a convenient API where you can create the mapped NSData, use it, and dispose of it normally. Any extra cleanup should just <em>happen</em>.
