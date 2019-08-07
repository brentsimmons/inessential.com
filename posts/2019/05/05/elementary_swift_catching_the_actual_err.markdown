@title Elementary Swift: Catching the Actual Error
@pubDate 2019-05-05 12:14:26 -0700
@modDate 2019-05-05 12:41:44 -0700
I’ve written 100,000 lines of Swift code, maybe? But, even after all this code, I still have a blind spot with Swift `try/catch`. I’m writing this up just in case you do too.

My problem was with getting the actual error in a `catch` block. When I learned that there was a magic `error` variable, my problem was partly solved, because I could do this: `catch { doSomething(with: error) }`.

So that’s what I always did. But then, just yesterday, I finally had a case where I wanted to catch a specific type of error — and I just couldn’t figure it out.

I looked at the [documentation on Swift error handling](https://docs.swift.org/swift-book/LanguageGuide/ErrorHandling.html), which shows catching a specific error type like this: `catch is VendingMachineError`. (That’s the actual example! No, I’m not writing code for vending machines.)

I figured that, inside the block, there would be that magic `error` variable, and it would be typed as `VendingMachineError`. Like this: `catch is VendingMachineError { doSomething(with: error) }`.

Nope! That’s not how it works. The magic `error` variable does *not* exist in this case.

So…

I asked some friends — [Dave DeLong](https://davedelong.com/blog/) and [Tim Ekl](http://www.timekl.com/) — who helped me. The answer was this:

	catch let error as VendingMachineError { doSomething(with: error) }

The key to this is that you use [Swift patterns](https://docs.swift.org/swift-book/ReferenceManual/Patterns.html) with the `catch`, and Swift patterns support variable binding. But patterns are a topic I don’t fully get yet, either.

(For instance, why do we use `case` sometimes outside of a `switch`? I don’t actually know.)

<p style="text-align:center">* * *</p>

Anyway. This post has four points. One is to help anyone else who runs across this problem. Hopefully a search will land them here.

The second is to suggest that the Swift error-handling documentation really should have this as an example — catching an error of a specific type, and getting a reference to that variable, is (or should be) a common thing to want to do.

The third is a reminder that even long-time programmers are still sometimes learning basic stuff. If your brain likes to justify your impostor syndrome with various tests — like “I’m not a *real* programmer till I know everything about Swift” — then tell your brain to hit the road.

The last is a reminder that having smart friends is always a good idea. :)
