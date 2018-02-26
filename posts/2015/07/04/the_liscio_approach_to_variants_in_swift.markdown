@title The Liscio Approach to Variants in Swift
@pubDate 2015-07-04 17:39:59 -0700
@modDate 2015-07-04 17:39:59 -0700
In two recent posts — see how we [keep calm and carry on](https://twitter.com/jaredsinclair/status/616658219524587520)? We’re back to tech topics — I wrote about implementing variants in Swift 2.0.

(See [Swift question: Enum vs. Struct for Variants](http://inessential.com/2015/06/23/swift_question_enum_vs_struct_for_vari) and, before that one, [Swift Protocols Question](http://inessential.com/2015/06/21/swift_protocols_question).)

In both cases I was definitely thinking like an Objective-C programmer — I was thinking about how to wrap native types in a variant type.

One approach was to use an enum with associated types, which is much like using tagged unions in C. Another approach was to create a different struct for each under-the-hood value type and have them all conform to a Value protocol.

[Chris Liscio](https://twitter.com/liscio?lang=en) — [Capo](http://supermegaultragroovy.com/products/capo/) author (Capo is genius, FYI) — suggested another approach: *Don’t wrap.* Don’t box. Just use the native types directly.

That is, instead of creating something like this…

<code>protocol Value {</code><br />
<code>&nbsp;&nbsp;func valueBySmashingOtherValue&#8203;(value: Value) -> Value</code><br />
<code>}</code>

<code>BoolValue : Value {</code><br />
<code>&nbsp;&nbsp;let value: Bool</code><br />
<code>&nbsp;&nbsp;func valueBySmashingOtherValue&#8203;(value: Value) -> Value {</code><br />
<code>&nbsp;&nbsp;&nbsp;&nbsp;// do something and return a Value</code><br />
<code>&nbsp;&nbsp;}</code><br />
<code>}</code>

<code>IntValue : Value {</code><br />
<code>&nbsp;&nbsp;let value: Int</code><br />
<code>&nbsp;&nbsp;func valueBySmashingOtherValue&#8203;(value: Value) -> Value {</code><br />
<code>&nbsp;&nbsp;&nbsp;&nbsp;// do something and return a Value</code><br />
<code>&nbsp;&nbsp;}</code><br />
<code>}</code>

etc.

…do this instead:

<code>protocol Value {</code><br />
<code>&nbsp;&nbsp;func valueBySmashingOtherValue&#8203;(value: Value) -> Value</code><br />
<code>}</code>

<code>extension Bool : Value {</code><br />
<code>&nbsp;&nbsp;func valueBySmashingOtherValue&#8203;(value: Value) -> Value {</code><br />
<code>&nbsp;&nbsp;&nbsp;&nbsp;// do something and return a Value</code><br />
<code>&nbsp;&nbsp;}</code><br />
<code>}</code>

<code>extension Int : Value {</code><br />
<code>&nbsp;&nbsp;func valueBySmashingOtherValue&#8203;(value: Value) -> Value {</code><br />
<code>&nbsp;&nbsp;&nbsp;&nbsp;// do something and return a Value</code><br />
<code>&nbsp;&nbsp;}</code><br />
<code>}</code>

etc.

That is, *extend* the native types instead of wrapping them.

In Objective-C you can’t extend BOOL or NSInteger since they’re not object types, but in Swift you *can* extend Bool and Int and similar types.

At my stage in learning Swift I wouldn’t have thought of this — but Chris did. (Thanks, Chris!)

(The advantages of this approach are, I hope, self-evident.)

PS The code above hasn’t been checked to see if it compiles. (Written directly in MarsEdit.) But you get the idea.

PPS I am frequently tempted to write that *Objective-C is my lightsaber*. But I don’t think that’s fair. I think it’s more that I’m still learning how Swift can be elegant — and Chris’s approach here counts as an instance of elegance.
