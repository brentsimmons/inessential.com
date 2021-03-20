@title When DispatchQueue.main.async Is Not Your Friend
@pubDate 2021-03-19 18:24:59 -0700
@modDate 2021-03-19 18:26:40 -0700
You already know, of course, that you need to run UI code on the main thread. Pretty much anything to do with UIKit or AppKit needs to run on the main thread.

And so, in strategic places, you use `DispatchQueue.main.async` to run some code on the main thread.

All good, you figure. Do a PR, move to the next ticket.

But here’s the thing you may not realize: the intent here is actually ambiguous, and it may not work as you expect. It can even lead to crashing bugs!

#### Async means async

Consider this code running on the main thread:

	print("1")
	print("2")
	DispatchQueue.main.async {
	  print("3")
	}
	print("4")

What do you think the result is?

It’s:

	1
	2
	4
	3

This means that the `.async` truly *is* async. It’s not making an exception when the code is already running on the main thread.

Consider that same code running in a loop three times. You’d get something like:

	1
	2
	4
	1
	2
	4
	1
	2
	4
	3
	3
	3

There’s a difference in intent between 1) running code immediately if on the main thread, async otherwise, and 2) always async.

`DispatchQueue.main.async` is, as you’d expect, always async, and that can be a problem.

#### Crashing Bug

I can think of at least one way this might crash. Suppose you have a table view or collection view, and the model gets updated out of order, which leads to an exception about an index out of range or whatever — because that async call means that the model was actually not updated when you thought it was.

You can probably think of other possible crashing bugs. At the very least, you’re leaving yourself open to code-ordering misunderstandings.

#### What To Do

You want the equivalent of this:

	if (Thread.isMainThread) {
	  someCode()
	}
	else {
	  DispatchQueue.main.async {
	    someCode()
	  }
	}

You don’t want to write all that every time, though. You can of course create a reusable function that takes a block of code and then runs it right away or via the async call.

If I’ve just solved your mystery crash with your collection view, then go buy some indie software like [Acorn 7](https://flyingmeat.com/acorn/). :)
