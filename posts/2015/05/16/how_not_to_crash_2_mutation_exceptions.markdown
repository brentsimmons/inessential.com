@title How Not to Crash #2: Mutation Exceptions
@pubDate 2015-05-16 09:48:11 -0700
@modDate 2015-05-16 09:50:36 -0700
You get a collection from somewhere and enumerate it — and then you get an error about the collection being mutated as it was being enumerated. The app crashes.

You can avoid this unhappy fate with one simple trick: don’t enumerate mutable collections.

#### Disagree with me

You might hold the reasonable position that the *real* answer is not to mutate a mutable collection while enumerating it. You should have enough understanding of your app to be able to write code that safely enumerates a mutable collection.

Yes, you should. You absolutely should.

However: writing crash-free code is about removing doubt. It’s about minimizing the chances for errors, and minimizing the chance that future changes (by you or somebody else) introduce a crash.

#### Mutable collections should not be part of public API

It should be extremely rare — or, better, *never* — that an object has a public property that is a mutable collection. Mutable collections should be internal to the object.

(Furthermore, as much as possible, public collections should be read-only. This isn’t always possible, of course.)

Now, it’s entirely likely that an object has a public collection that is internally a mutable collection. Think of an object that tracks operations. It might make the following public:

<code>@property (nonatomic, readonly) NSArray \*operations;</code>

And internally there’s this:

<code>@property (nonatomic) NSMutableArray \*mutableOperations;</code>

<code>- (NSArray \*)operations {</code><br />
<code>&nbsp;&nbsp;return self.mutableOperations;</code><br />
<code>}</code>

That’s perfectly legal code: because mutableOperations is an NSMutableArray, it’s also an NSArray. (I did it this way for years. I thought to myself, “Hey, I’m a grownup. I can *handle* it.” But what I didn’t realize was that grownup developers write code to make errors less likely.)

#### Properties specified as immutable should be immutable in fact

In the above example, you’re advertising <code>operations</code> as an array that can be enumerated safely at any time. Another person — or you yourself, looking at this in six months — won’t necessarily realize that really you’re getting back a mutable array that *can’t* necessarily be safely enumerated.

Here’s the truth-in-advertising solution:

<code>- (NSArray \*)operations {</code><br />
<code>&nbsp;&nbsp;return [self.mutableOperations copy];</code><br />
<code>}</code>

(It wouldn’t hurt to modify the property declaration also to make it clear that it’s a copy, but I admit that I don’t always do that. It would have the advantage of making it completely clear to the user of the API what’s going on.)

You might push back, citing performance or memory use issues or both — but I’ll admit something: I’m a performance junkie, and I spend an inappropriate amount of time in Instruments making sure things are fast and use a non-weird amount of memory. And I’ve never, ever found this to be a problem. If your app has performance or memory use issues, the problem is something else, not these copies. (Though you might consider using <code>@autoreleasepool</code> so that these copies don’t last very long.)

Make the copy.

#### Bonus points: don’t believe their lies

I recently fixed a mutation error when enumerating NSTextStorage layoutManagers:

<code>@property (readonly, copy) NSArray *layoutManagers;</code>

*Obviously* it’s safe to enumerate. It’s an NSArray, it says, and it’s a copy. Cool. Enumerate away.

But it’s a lie. In the debugger I found that it’s an NSMutableArray (__NSArrayM) — and that it’s not a copy at all. It’s NSTextStorage’s <code>\_layoutManagers</code> instance variable, which is declared as an NSMutableArray.

And some code in my enumeration block did a thing that triggered a mutation in layoutManagers, and the app crashed.

The answer: enumerate a copy of layoutManagers. Problem solved.

There’s a general point: if you’re getting a collection from code that isn’t yours, it doesn’t hurt to be defensive and enumerate a copy.
