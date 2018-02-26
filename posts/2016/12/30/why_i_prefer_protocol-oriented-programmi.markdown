@title Why I Prefer Protocol-Oriented-Programming in Objective-C to Swift
@pubDate 2016-12-30 15:42:31 -0800
@modDate 2016-12-30 15:42:31 -0800
I first learned protocol-oriented-programming with Objective-C, and I was very pleased to see the Swift team emphasize this style.

But, at least at this writing at the end of 2016, I still run into problems when I use this style of programming in Swift.

Here’s the problem I’m trying to solve:

#### Variant Value

I’m working on a schema-less hierarchical database. Tables can contain tables, and they can contain values such as strings, numbers, booleans, dates, arrays, and so on.

To represent these values, I’d rather use a Value protocol rather than a Value class. If it’s a protocol, then I can have completely separate implementations: BoolValue and DateValue and ArrayValue and so on would conform to Value, but otherwise would have different implementations.

But here’s the thing: ArrayValue needs to have an actual Swift array of type `[Value]`.

So let’s say you want to add something to that Swift array, where arrayValue is of `[Value]` type. Let’s say you’ve created `trueValue`, which is a `BoolValue`, and `BoolValue` conforms to the `Value` protocol.

<code>arrayValue += [trueValue]</code>

You *can’t*. Because even though `BoolValue` conforms to the `Value` protocol, this isn’t handled automatically. The compiler knows all the types involved, but it still won’t let you do this unless you explicitly cast. The following works:

<code>arrayValue += [trueValue as Value]</code>

In Objective-C, no casting is required:

<code>[arrayValue addObject:trueValue];</code>

This may seem like nitpicking on my part, but that added bit of housekeeping makes protocol-oriented-programming in Swift feel a little bit unnatural.

A natural form of protocol-oriented-programming might start with this premise: any time the protocol type is called-for, you can use an object that conforms to that protocol.

#### More complexity, to push the point

Let’s say you have two arrays:

<code>let array1 = [trueValue as Value]</code><br />
<code>let array2 = [trueValue]</code>

You and I both know that those arrays contain just one object, and it’s an identical object. Those two arrays are absolutely equal.

But you can’t compare them:

<code>array1 == array2</code> will not compile, because array1 is of type `[Value]` and array2 is of type `[BoolValue]`. Even though BoolValue conforms to Value, this won’t work.

In Objective-C, you’d just use `isEqual:`, and it would work as expected.

But it gets worse:

<code>let array1 = [trueValue as Value]</code><br />
<code>let array2 = [trueValue as Value]</code>

Okay: now you *know* those two arrays couldn’t possibly be more equal.

But <code>array1 == array2</code> *still* won’t compile, and you’ll get the following error:

<code>binary operator '==' cannot be applied to two '[Value]' operands</code>

In Objective-C, you’d write:

<code>NSArray \*array1 = @[trueValue];</code><br />
<code>NSArray \*array2 = @[trueValue];</code>

And <code>[array1 isEqual:array2]</code> will return YES.

(You could type those arrays using lightweight generics, and the outcome is the same: it works.)

So: a second premise for natural protocol-oriented-programming might be: a protocol-conforming object should have the same features as other objects — for instance, you should be able to make it Equatable (the equivalent of, in Objective-C, responding to `isEqual:`).
