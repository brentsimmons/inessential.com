@title Solving Problems I Don’t Have, Except that I Do Have Them
@pubDate 2015-07-19 12:29:55 -0700
@modDate 2015-07-19 12:32:59 -0700
I’m not sure if I’ve said it on my blog, but I’ve said it in person to other people: Swift’s type system solves a problem I don’t have.

Example: if I make an NSArray, I know what’s in there, my code knows what’s in there, and I’ve never had a crash or other bug where the array contained something unexpected.

Seriously. This isn’t that hard.

Except that that’s not actually true.

<p style="text-align:center">* * *</p>

There are two cases where that hasn’t been true, and they’re representative, I think.

One is in JSON parsing: I’ve ended up with NSNull in an array or dictionary where I expected something else — and then I’ve sent it a message expecting it to be an NSString or whatever, and the app crashed.

So that’s a thing: data from the outside world may be weird.

That being said, Swift doesn’t necessarily help very much. Or maybe it does, but I’m not good enough at Swift yet to realize how it helps. Totally possible. But right now, for me, there’s always a point where I’m surprised to be forcing a cast and then looking around nervously to see if the atmosphere ignited.

There’s a second case where I think it *does* help. I wrote a crashing bug in Objective-C (and fixed it moments later; it didn’t ship) where I expected everything in an NSArray to be of the same type, and it wasn’t true.

The code was building a pull-down menu, and the zeroth item was an NSDictionary with a value for key @"name", and other items were of an object type that had a name property. Every object would respond to <code>valueForKey:@"name"</code> as expected — but not to `obj.name`. I didn’t realize what was going on at first, and Swift absolutely would have helped.

Now — the original code wasn’t written by me, and I wouldn’t have done it that way, but it’s not necessarily *wrong*. Just different from my style.

But it’s a fact of life that apps very often have more than one author, and sometimes many more than one, and with different styles. And they may be separated in time (the original author may not even be working on that app; they may not even be at the company any more).

While Swift makes it harder to write type-related bugs — which is *great* — it also makes it harder, sometimes, to do what I want in a reasonable and simple way, which is not great.

However, it improves with each release. And if there are trade-offs which make the choice of language a tie, the tie-breaker has to be the question: which technology is the future?

(That presumes that the choice of language is a tie. It may or may not be. It differs with each person and each app, and it changes with every release of Swift.)
