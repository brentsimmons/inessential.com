@title Copy vs. Strong NSArray Properties
@pubDate 2016-06-30 14:07:02 -0700
@modDate 2016-06-30 14:08:11 -0700
At work this morning I added a property to an Objective-C object that looked something like this:

<code>@property (nonatomic, strong) NSArray \*someArray;</code>

And then it was suggested to me that `copy` would be better than `strong` in this case.

I have nothing against `copy` — but with an *immutable* array, is that really necessary? The array can’t change, so why copy it?

Well… that’s not strictly true. A caller could use an `NSMutableArray` — which would be perfectly valid — but then hold on that array and mutate it later on, which would be dumb.

So I ask: who would write code like that?

It’s not a class of mistake that I personally make. (I’ve internalized this so completely from years of writing Objective-C. I do make other classes of mistakes, of course.)

And then I think “Who would write code like that?” is the wrong question. The real question is, “Why wouldn’t I write code that minimizes the effect of a possible mistake?”

(Or even *not* a mistake. It could be entirely legitimate that the caller has a mutable array that it holds on to and mutates later on.)

<p style="text-align:center">* * *</p>

This makes me wonder about the difference between code I write for myself and code I write as part of a team. Since I know that I wouldn’t make this particular mistake, I can safely use `strong` instead of `copy` in my own code.

But, really — sharp right turn here; buckle up! — doesn’t it make me wish everything was already in Swift, so we’d have the safer behavior automatically?

Yes. Yes it does.

My personal projects are mostly in Swift — converted to Swift 3 already — but, for obvious reasons, at work we often write new code in Swift but still have a large Objective-C codebase.

What I don’t need in life — because it adds complexity, and I don’t have time for that — is three separate coding styles: Swift, my Objective-C, and work Objective-C.

The only one I can get rid of is “my Objective-C.”

Okey-doke.
