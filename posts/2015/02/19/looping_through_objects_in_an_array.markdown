@title Looping Through Objects in an Array
@pubDate 2015-02-19 15:15:55 -0800
@modDate 2015-02-19 15:28:45 -0800
One way to loop through objects and stop when you’ve found the one you want is the following:

<code>for (id oneObject in someArray) {</code><br />
<code>&nbsp;&nbsp;if ([oneObject passesTest]) {</code><br />
<code>&nbsp;&nbsp;&nbsp;&nbsp;return oneObject;</code><br />
<code>&nbsp;&nbsp;}</code><br />
<code>}</code>

The <code>return</code> could as well be a <code>break</code> statement. And the code in Swift would be something like this (typed without compiling; probably has errors, but you get the point):

<code>for oneObject in someArray {</code><br />
<code>&nbsp;&nbsp;if oneObject.passesTest() {</code><br />
<code>&nbsp;&nbsp;&nbsp;&nbsp;return oneObject</code><br />
<code>&nbsp;&nbsp;}</code><br />
<code>}</code>

I’ve long been a fan of this. It’s easy to read and understand. It’s efficient because it stops as soon as the object is found.

It’s also pretty easy to make something re-usable: you could make a <code>firstObjectPassingTest:</code> category method that takes a block that performs the test. Easy.

In 10.6 Apple added <code>- (void)enumerateObjects&#8203;UsingBlock:&#8203;(void (^)&#8203;(id obj, NSUInteger idx, BOOL *stop))block;</code>

<a href="https://www.mikeash.com/pyblog/friday-qa-2010-04-09-comparison-of-objective-c-enumeration-techniques.html">Mike Ash</a>:

>For simple enumeration, the block syntax doesn't really offer any advantage over fast enumeration and the for/in syntax. The syntax is a bit clumsier, and iteration is a bit slower. The code has to call your block for every object. This overhead is less than that of a message send, as in the <code>NSEnumerator</code> case, but is more than the simple C for loop of <code>NSFastEnumeration</code>.

There are cases — dictionaries in particular — where the block-based enumeration can be the best choice. But most of the time the for-in enumeration is the straightforward and less clever approach. (“Less clever” is a good thing.) It’s faster too.

And yet… I’ve been afraid to say this out loud, as it seems to me that the entire world is on a we-love-blocks-and-hate-loops kick. (Back this up? I can’t. I love blocks too, but I have nothing against loops, and I’ll take the simple, clear, readable loop over a blocks-based method when it makes sense, which is almost every time, though not *every* time.)

And then today there was <a href="https://devforums.apple.com/message/1105131#1105131">this response from Chris Lattner</a> (message #11). I can’t quote it because it’s on the confidential Apple forums. But I bet anybody who’s read this far also has access to the forums and knows who Chris Lattner is.

And now I feel better about for-in loops.
