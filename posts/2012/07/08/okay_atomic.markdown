@title Okay Atomic
@pubDate Sun Jul 08 14:17:38 -0700 2012
@modDate Tue Jul 17 10:54:23 -0700 2012
I have habitually declared my properties as <code>nonatomic</code>. Exceptions are <em>extremely</em> rare.

Since <code>atomic</code> is the default, I have to do this:

<code>@property (nonatomic, strong) NSString *foo;</code>

But it occurs to me now that switching to <code>atomic</code> will not be a performance issue. It makes sense to stick with <code>nonatomic</code> for things like Core Data objects — but it isn’t really needed for things like IBOutlets and other properties that are not frequently set.

Since it isn’t really needed in those cases, I could just go with the default and save myself a little typing and a little code.

<code>@property (strong) NSString *foo;</code>

Hmmm. Looks naked, but I could get over that.

<em>Update 3:12 pm:</em> I just learned that <code>strong</code> is the default for properties since Xcode 4.3.

Which means I could do this:

<code>@property NSString *foo;</code>

I <em>like</em> less code. It looks shocking to me — <em>scandalous</em>, even — but I’d adapt.

<em>Update July 17, 2012:</em> I just couldn’t do it. I’m sticking with nonatomic — and still declaring explicitly as strong.
