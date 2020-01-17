@title Immutable Swift Structs
@pubDate 2020-01-16 20:52:48 -0800
@modDate 2020-01-16 21:00:24 -0800
As you read this, consider that I might be a squirrel and not, as I like to pretend, a rational programmer.

#### My Two Brains

My Objective-C brain — which will never leave me, even though I’ve been writing in Swift for years now — always told me to create immutable objects as often as possible.

Objective-C brain says, “Immutable means you never have to worry about it.”

My Swift brain — which is newer, and has all the fun these days — tells me another thing.

Swift brain says, “Value types are good. Use value types as often as possible.”

So my favorite thing in all of Swift is an immutable struct. It’s a value type, and it can’t be mutated!

Both brains happeeee! 🐥🐣

#### Val vs. Let

This came up in working on NetNewsWire: some model objects — some structs decoded from JSON returned by a syncing server — used `var` instead of `let` for their properties.

These model objects are not mutated anywhere. So, I figured, those declarations should use `let` instead. (Which would make my brains happy!)

An immutable struct is, after all, the greatest thing ever, right? You don’t have to worry about it. It never gets copied (at least in theory). If you share it across threads, it’s the same everywhere: you don’t get some number of different copies.

So I asked the author to change the `var`s to `let`s.

I didn’t expect the response — which was “Why?” (Asked earnestly, of course.)

I struggled with the answer.

#### Value Types Are Good

Here’s the thing: value types *are* good. Even though those structs aren’t being mutated *now*, we could imagine cases where they could be.

Why not leave it up to the code that has one of these to decide to mutate or not? After all, as value types, this makes a copy and doesn’t affect other instances. Value types are safe, regardless of mutability.

And yet…

#### Here’s Where I Might Be a Squirrel

I still insisted on using `let` for the properties in these structs.

There’s something to be said, of course, for always starting out strict and loosening up only when it’s actually needed. Don’t loosen up in anticipation. But that’s hardly a big deal here.

Instead I think it goes to code-reading: if I see `let` instead of `var`, I have some understanding of the intent. In this case, the structs are parsed versions of stuff-from-the-server, and that’s a case where you could expect immutability, and be surprised to find something else.

Those structs don’t get saved anywhere as-is; they don’t live long; nothing the user does can change them.

These structs are a report: “Server says this.”

So… I think it’s the right call, but I’m absolutely aware of the possibility that I’m just distracted by my Objective-C instincts, and I’m over-tidying.

I don’t know! What do you think? Should I have left it as-is?
