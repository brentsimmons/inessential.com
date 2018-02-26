@title Swift question: Enum vs. Struct for Variants
@pubDate 2015-06-23 19:33:44 -0700
@modDate 2015-06-23 19:35:20 -0700
In a <a href="http://inessential.com/2015/06/21/swift_protocols_question">previous post</a> I mentioned using structs plus a protocol to implement a variant type. There’s a Value protocol and a number of different structs that conform to that protocol.

But <a href="https://gist.github.com/andymatuschak/a40c4c699c0abdd704ce">Andy Matuschak’s comment</a> about using an enum instead keeps coming to mind. And then there’s this note in the <a href="https://itun.es/us/k5SW7.l">pre-release Swift book</a>:

> Alternatively, enumeration members can specify associated values of <em>any</em> type to be stored along with each different member value, much as unions or variants do in other languages.

So let’s imagine a variant that can represent a bunch of different data types and that has logic for arithmetic operations and for coercions.

<code>enum Value {</code><br />
<code>&nbsp;&nbsp;case variantBool(Bool)</code><br />
<code>&nbsp;&nbsp;case variantInt(Int)</code><br />
<code>&nbsp;&nbsp;case variantString(String)</code><br />
<code>&nbsp;&nbsp;etc. — for doubles, dates, data, collections, and so on</code><br />
<code>}</code>

(Forgive the “variant” prefix in this example — it’s there so I’m not writing `case Bool(Bool)` and so on.)

Now let’s say we have a bunch of logic.

<code>func canAddValue(value: Value) -> Bool</code><br />
<code>func valueByAddingValue&#8203;(value: Value) -> Value</code><br />

And so on for subtracting, multiplying, and dividing. (Example: variantStrings can add and subtract other variantStrings and things that can be coerced to variantStrings, but they can’t multiply or divide. variantData can’t do any arithmetic at all. Etc.)

And then add logic for coercions:

<code>func canCoerceToType&#8203;(type: Value) -> Bool</code><br />
<code>func valueByCoercingToType&#8203;(type: Value) -> Value</code>

(This is a little weird because a Value is a type — variantBool, variantInt, etc. — as well as data.)

There’s a whole ton of logic there: a variantDate can be coerced to a variantDouble but not to a variantArray, etc.

Unless I’m missing something — *which is highly likely*, as I’m just barely starting — I’ve got a whole ton of switch statement to write. And those switch statements have inner switch statements. (Conceptually, that is. Of course I would break things out into separate functions, as in <code>func variantBool&#8203;CanCoerceToType&#8203;(type: Value) -> Bool</code> and so on.)

That seems a lot to me like writing C code with tagged unions. Which is not necessarily a bad thing — I grew up on C and and still love programming in C (though I don’t get much chance to do it these days).

My original idea — a Value protocol plus a bunch of structs conforming to Value, one for each type — is something an Objective-C developer who’s new to Swift would come up with.

I realize it’s still early to ask about idiomatic Swift and best practices, but I’m asking anyway. What would you do?
