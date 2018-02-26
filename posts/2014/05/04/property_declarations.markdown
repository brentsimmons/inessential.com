@title Property Declarations
@pubDate 2014-05-04 15:05:35 -0700
@modDate 2014-05-04 15:09:03 -0700
I’ve had a few different conventions for how I declare properties.

Here’s how I do it these days:

If it’s strong, I omit the `strong` keyword, since properties are strong by default.

<code>@property (nonatomic) NSDate \*dateCreated;</code>

I always put `nonatomic` first (and almost every single property is nonatomic), so things line up a little better:

<code>@property (nonatomic) NSDate \*dateCreated;</code><br />
<code>@property (nonatomic, weak) NSArray \*notes;</code><br />
<code>@property (nonatomic, assign) NSUInteger numberOfCats</code>

`readonly` and `readwrite` come last:

<code>@property (nonatomic, assign, readwrite) CGFloat heightInCubits;</code>

I find that this helps me understand quickest. My brain filters out the `nonatomic` part. Strong is the most common thing and thus omitted, which makes it easier to pick out `weak`, `assign`, `readwrite`, and `readonly`.

I never use the `getter=` thing, because I find it easier when the getter and setter have the same name. It’s too much to remember when there’s a custom getter name.

PS I don’t mean that I order the properties in any particular order, though. It could look like this:

<code>@property (nonatomic, assign, readwrite) CGFloat heightInCubits;</code><br />
<code>@property (nonatomic, weak) NSArray \*notes;</code><br />
<code>@property (nonatomic, assign) NSUInteger numberOfCats</code><br />
<code>@property (nonatomic) NSDate \*dateCreated;</code>
