@title Swift Protocols Question
@pubDate 2015-06-21 10:55:44 -0700
@modDate 2015-06-22 11:51:55 -0700
I’m still very much a Swift newbie.

The following example is contrived, but it accurately depicts the problem I’m trying to solve.

I have a protocol:

<code>protocol Value: Equatable</code>

A number of different structs conform to this protocol. Some of those structs also conform to this protocol:

<code>protocol Smashable {</code><br />
<code>&nbsp;&nbsp;func valueBySmashing&#8203;OtherValue&#8203;(value: Value) -> Value</code><br />
<code>}</code>

My intent is absolutely clear — `valueBySmashingOtherValue` must return an object that conforms to the Value protocol.

However, I get this error: <code>Protocol 'Value' can only be used as a generic constraint because it has Self or associated type requirements.</code>

Okay. So I revise the Smashable protocol like this:

<code>protocol Smashable {</code><br />
<code>&nbsp;&nbsp;func valueBySmashing&#8203;OtherValue&#8203;&lt;T>(value: T) -> T</code><br />
<code>}</code>

That compiles. Cool.

So in a struct named `Foo` I add this:

<code>func valueBySmashing&#8203;OtherValue&#8203;&lt;T>(value: T) -> T {</code><br />
<code>&nbsp;&nbsp;return Bar()</code><br />
<code>}</code>

That’s right — Foo’s &#8203;valueBy&#8203;Smashing&#8203;OtherValue returns a Bar. (Yes, this is contrived, but it distills the more-complex real-world code, which makes sense and is absolutely the right thing to do.)

Both conform to `Value`.

But I get this error on the `return Bar()` line: <code>'Bar' is not convertible to 'T'.</code>

At this point I don’t know what to do. Hence this blog post.

#### Objective-C version

I approach Swift exactly like an Objective-C coder — because I’ve been writing Objective-C for almost 15 years. Here’s the Objective-C version:

<code>@protocol Value&lt;NSObject></code><br />
<code>*stuff*</code><br />
<code>@end</code>

<code>@protocol Smashable&lt;NSObject></code><br />
<code>- (id&lt;Value>)valueBy&#8203;SmashingOtherValue:&#8203;(id&lt;Value>)&#8203;otherValue;</code><br />
<code>@end</code>

`Foo` method (`Foo` and `Bar` both conform to `Value`):

<code>- (id&lt;Value>)valueBy&#8203;SmashingOtherValue:&#8203;(id&lt;Value>)&#8203;otherValue {</code><br />
<code>&nbsp;&nbsp;return [[Bar alloc] init];</code><br />
<code>}</code>

#### One possibility

I’m still thinking in Objective-C. It’s entirely likely that there’s a Swift-like design that hasn’t occurred to me. But what is it?

One simple possibility: don’t use protocols at all. Make a `Value` struct that does everything the various Value-conforming structs currently do. The `Value` struct would be littered with switch statements, which is ugly (and is usually a sign of poor design), but it would work.

This doesn’t seem Swift-like, though, given the [importance of protocols to Swift](https://developer.apple.com/videos/wwdc/2015/?id=408). And I can’t make myself do it.

There must be a better option.

What I don’t want to do is complain, a la Nabokov, that this new language can’t match the suppleness of my native language. I’d rather assume it’s just that I haven’t learned this new language well enough.

P.S. I’ll happily link to your blog post if you write up a solution.

<i>Update 10:30 am Monday June 22</i>:

#### Answers

There are a bunch of <a href="https://twitter.com/brentsimmons/status/612682015071080448">replies on Twitter</a>.

The essence of the best answers was this: `Value` should not be `Equatable` — the <em>individual structs</em> should be `Equatable`.

<a href="https://twitter.com/brentdax/status/612692374922350592">Brent Royal-Gordon</a>:

> Thinking more, the problem is Equatable. Remove or abstract that conformance from Value and everything will work right.

For more details, see <a href="http://owensd.io/2015/06/22/re-inessential-swift-protocols.html">David Owens II</a>’s blog post: 

>…there is a way out of this if your situation allows for it: don’t conform your protocol to `Equatable`, instead, conform your types to it.

And <a href="http://www.llamagraphics.com/content/combining-swift-protocols">Llamagraphics</a>’s blog post:

> The error message says *Protocol ‘Value’ can only be used as a generic constraint because it has Self or associated type requirements*. This is a little misleading, because it implies that valueBySmashingOtherValue needs to be rewritten as a generic function, but that actually just pushes the problem down to the adopters of the Value protocol. The real ﬁx is to move the use of the Equatable protocol from the Value protocol to the individual struct declarations…

And see <a href="https://gist.github.com/andymatuschak/a40c4c699c0abdd704ce">Andy Matuschak’s gist</a> — which makes an interesting point that I had briefly considered and then dropped:

> One note before we start: if the inhabitants of Value are a closed set, then making Value an enum is going to be a clearer model than using a protocol like this. I'm assuming you need to be able to retroactively add new members of Value.

In my case, the inhabitants of Value *are* a closed set. There are about a dozen.

What concerned me, though, is that I’d be creating a monster enum with a whole bunch of switch statements. But perhaps that’s not true? I don’t know Swift well enough to think it out in advance — I’d have to try it and see.

(Actually, I may be misunderstanding Andy. There are a dozen Value types — but the values are unbounded. Perhaps not a great case for an enum.)

#### Ramble

In the end, I’m still tempted to say the Objective-C version was simpler. And it is, and not just because I’m more familiar with Objective-C. But it’s important to note that it’s not apples-to-apples. In Objective-C I’m creating classes instead of structs, and there’s no support for the == operator.

But I will say this: Objective-C, because it’s less strict with types, is closer to a scripting language than Swift is.

I know that that could be controversial, and seems absurd when you consider that Objective-C is a superset of C, which is pretty darn far from a scripting language. But Objective-C as-we-mostly-write-it doesn’t include much straight C code.

That’s not a value judgment but a characterization. There is a place for strict, less-strict, and not-strict-at-all languages — they all have their uses.

But when I imagined Apple’s next-generation language, I imagined a higher-level and less strict language — one that made it easier to get started as a developer, one that got rid of a bunch of the housekeeping we have to do as Objective-C developers.

Though Swift does get rid of a bunch of housekeeping — we can use type inference much of the time, we don’t have to create .h files, etc. — it adds its own housekeeping mandated by a stricter type system (and optionals).

When I think about how much of our apps is user interface code — which is often rather boring to write and is just stuff like setting a label, animating a property, pushing a view controller, and so on — I wonder why we’re not using an actual scripting language. It wouldn’t have to be for *all* of a given app — not for the performance-sensitive parts — but it would be great for all the stuff that’s just pushing user interface APIs around.
