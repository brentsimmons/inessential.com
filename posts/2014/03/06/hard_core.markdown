@title Hard Core
@pubDate 2014-03-06 17:02:42 -0800
@modDate 2014-03-06 17:04:30 -0800
<a href="http://waffle.wootest.net/2014/03/07/hard-core/">waffle</a>:

>It’s true; other platforms do suffer from not having quite a few elegant solutions present in Cocoa. (Oh, to have every object solve key-based archiving/coding abstractly, so that you can get universal coverage with your own serialization engine; <code>NSCoding</code> is the most underappreciated piece of design in all of Cocoa.) And it is very neat when it all works. But what about when it doesn’t?

I should explain why I chose not to use Core Data this time. (Note that I <em>have</em> shipped apps that use Core Data.)

This time it wasn’t the pathological cases like marking 10,000 items as read. Instead it’s two things.

The first is concurrency. I’ve been working with multi-threaded database systems since the mid ’90s, and I understand the issues very well.

I understand the issues well enough to know that every opportunity I can take to simplify concurrency issues to the point <em>where concurrency isn’t an issue</em> is worth taking. (As long as it performs well and doesn’t harm the user experience.)

This becomes even more important when you add something complex — such as syncing — to the mix.

The second reason has to do with my enduring love of plain-ol’ Cocoa. I like regular Cocoa objects. I like being able to implement <code>NSCoding</code>, override <code>isEqual:</code> and <code>hash</code>, and design objects that can be created with a simple <code>init</code> (when possible and sensible). I <em>especially</em> like being able to do those things with model objects. (Which totally makes sense.)

And I prefer APIs like this…

<code>- (VSTag \*)existingTagWithName:(NSString \*)name;</code><br />
<code>- (VSTag \*)tagWithName:(NSString \*)name;</code><br />

…to APIs like this:

<code>- (VSTag \*)existingTagWithName:(NSString \*)name context:(NSManagedObjectContext \*)context</code><br />
<code>- (VSTag \*)tagWithName:(NSString \*)name context:(NSManagedObjectContext \*)context error:(NSError \*\*)error;</code><br />
