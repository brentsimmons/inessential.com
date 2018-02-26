@title Dave on Frontier
@pubDate 2014-06-19 11:38:45 -0700
@modDate 2014-06-19 11:39:42 -0700
In [Thinking out loud about Frontier](http://scripting.com/2014/06/19/thinkingOutLoudAboutFrontier.html), Dave Winer suggests porting the database code to JavaScript.

I hadn’t thought of that. It would probably be faster than you think. The bottleneck should be reading from and writing to disk, not the speed of the code itself.

Chuck Shotton (author of MacHTTP and WebSTAR) has a good comment on Dave’s post. Part of it:

>The major value proposition is the tight integration of persistent data store within the name space of the embedded scripting language and the ability to store and execute code from that database…

>The productivity gains are enormous, being able to write in a widely supported language using an easily-exported data model. For some reason, no one has really replicated the Frontier model using modern software stacks.
