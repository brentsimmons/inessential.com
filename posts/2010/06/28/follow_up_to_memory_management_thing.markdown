@title Follow up to memory management thing
@categoryArray Cocoa-Development
@pubDate Mon Jun 28 13:41:04 -0700 2010
@modDate Mon Jun 28 17:51:51 -0700 2010
In the <a href="http://inessential.com/2010/06/28/how_i_manage_memory">previous post</a> I have an initWithString method that looks like this:

<pre>- (id)initWithString:(NSString *)aString {
    self = [super init];
    if (self == nil)
        return nil;
    something = [aString retain];
    return self;
}</pre>

I knew, as I was typing it, that I’d get some feedback along the lines that I should use <em>copy</em> instead of <em>retain</em>.

And I did.

And it’s excellent advice, totally, no question. The reason to use <code>copy</code> instead of <code>retain</code> is because it enforces the expected immutability of that incoming string, so the caller is free to change it in case it’s really a mutable string.

However, I don’t follow that advice. One reason is that, in my eight years of Cocoa programming, this has never been an issue. Not once have I run into a problem because I used <code>retain</code> instead of <code>copy</code> in a case like this.

The second reason is that I consider the use of <code>copy</code> here a case of overly-defensive programming. The effect would be to hide a bug, if one exists, and I wouldn’t want that.

Given those two reasons, it’s just bonus that using <code>retain</code> means avoiding the extra allocation that using <code>copy</code> would mean — but I’ll take that bonus.

<em>Update 5:24 pm:</em> Yes, <em>copy</em> returns <em>self</em> for immutable objects. (All the time, at least for Foundation objects? I don’t know.) So, no bonus in those cases. But I myself often pass mutable objects where immutable is expected. So I get the bonus. (And it’s not a bug on my part, no.)

<em>Update 5:41 pm:</em> OK, why do I consider it a bug if aString is really a mutable string <em>and</em> I change it elsewhere? It’s totally legal if aString is really an NSMutableString. I do things like that all the time. But I code as if there’s an implicit contract: any Foundation objects (strings, dictionaries, arrays, sets, etc.) passed between objects must be treated as if immutable. If the object that receives the object wants to do something based on aString, it may, indeed, then have to make a mutableCopy or whatever. And if aString was really a mutable string, the caller has to not change it from that point on.

Why do I code this way? It simplifies things. It removes doubt.
