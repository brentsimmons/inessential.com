@title How I Manage Memory
@categoryArray Cocoa-Development
@pubDate Mon Jun 28 12:19:59 -0700 2010
@modDate Mon Jun 28 12:25:02 -0700 2010
I’ve noticed, in looking at other people’s Cocoa code over the years, that sometimes people still do weird things with retain, release, and autorelease — as if they’re not quite sure on the basics of memory management yet.

So I thought I’d talk about how I do things. There are three important points, then a practical explanation of one of them.

1. Overall memory use is a design issue. It’s not usually a case of over-using autorelease or something like that. (For instance: are all your objects in memory at all times, or do you use something like Core Data so you don’t have to do that?)

2. Memory management — the nuts and bolts of making sure you don’t leak or over-release — should be as simple as possible and done in the same way every time.

3. The exceptions to #2 should be done only as a result of profiling in Shark and Instruments.

<h4>Practical explanation of #2</h4>

I find not-leaking and not-over-releasing very, very easy. That’s because I have a simple system, and I do things the same way every time, except when profiling tells me I need to make an exception. (Which is rare.)

Here’s what I do:

I use properties, and I use the full form: <code>self.something</code> and <code>self.something = whatever</code>. I try to avoid custom accessor methods, just use the standard synthesized methods.

I don’t use the full form in <code>init</code> and <code>dealloc</code>, though, because it might trigger KVO or have other side effects.

So a made-up class might look like this:

<pre>
@interface BSThing : NSObject {
@private
	NSString *something;
}

- (id)initWithString:(NSString *)aString;

@property (nonatomic, retain) NSString *something;

@end

@implementation BSThing

@synthesize something;

- (id)initWithString:(NSString *)aString {
	self = [super init];
	if (self == nil)
		return nil;
	something = [aString retain];
	return self;
}

- (void)dealloc {
	[something release];
	[super dealloc];
}


- (void)someRandomMethodThatDoesStuff {
	//Let's just change something
	self.something = @"Something else";
}

@end
</pre>

Make sense? Outside of <code>init</code> and <code>dealloc</code>, access is always via <code>self.something</code>.

There are two other things I do:

<h4>Pretty much create everything as autoreleased</h4>

Seriously. I almost never write code like this:

<pre>
NSMutableDictionary *dict = &#91;[NSMutableDictionary alloc] init];
//do something with dict
[dict release];
</pre>

It’s more code and it complicates things and it’s easy to make mistakes. I get confused. I don’t understand at-a-glance that the code is correct. I know there is advice to avoid <code>autorelease</code> on iPhone — but you already know you can’t avoid it, and I’ve found that any drawbacks by use of <code>autorelease</code> are over-shadowed by other issues.

So here’s what I always write:

<pre>
NSMutableDictionary *dict = [NSMutableDictionary dictionary];
//do something with dict, completely un-worried about leaking it.
//I can even return early.
</pre>

<h4>Autorelease pools</h4>

One exception to the above is, of course, when you’re doing a bunch of allocations in a loop. Then I will use an inner <code>autorelease</code> pool. I won’t do that crazy thing where you make it drain every 10 times or whatever — I’ll drain it in each pass. Simpler — and no reason to change that unless Shark or Instruments says to change it.

I’ve been doing it that way since reading Mike Ash’s article <a href="http://www.mikeash.com/pyblog/autorelease-is-fast.html">Autorelease is Fast</a>. Though, obviously, it’s not as fast on iPhone, it’s still probably faster than you think it is.

<h4>Recap: my simple rules</h4>

1. Use properties, and use synthesized accessors as much as possible.

2. Always use the <em>self.something</em> form — no direct access to ivars, except in <code>init</code> and <code>dealloc</code>, where <em>only</em> direct access is allowed.

3. Create temporary objects, or objects that get returned by a method, as autoreleased.

4. Use autorelease pools as needed, but don’t try anything fancy.

5. Profile in Shark and Instruments, and make exceptions to the above only when it makes a real difference.

6. Consider that your overall memory use issues are probably design issues, not (usually) code issues.

Following these rules, writing Cocoa code is damn close to scripting.
