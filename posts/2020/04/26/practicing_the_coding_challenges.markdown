@title Practicing the Coding Challenges
@pubDate 2020-04-26 16:58:22 -0700
@modDate 2020-04-26 21:36:16 -0700
As part of my [job hunt](https://inessential.com/2020/03/31/looking_for_work) I’ve been doing some problems on [LeetCode](https://leetcode.com/) to prepare for coding challenges.

I don’t have a CS degree, but I have decades of experience — I know what a linked list is, for instance, and could one write one by hand easily if called to. In a few different languages, even. I could talk about the trade-offs between a linked list and a contiguous array. Etc. I’ve got all that.

But these tests are kicking my butt a little bit. I think I’ve figured out why.

Consider a question like this:

You need to add two numbers and get a sum. But, importantly, the digits of those numbers are stored in arrays, and they’re backwards.

The return value also needs to be in a backwards array.

If inputs are `[4,2,6]` and `[3,8,0,8]`, the function should return `[7,0,7,8]` — because `624 + 8083 == 8707`.

My style of coding is to break problems into steps and make it super-obvious to other people — and future-me — what the code is doing. I like to write code so clear that comments aren’t needed.

I’d start with a top-level function something like this:

	let num1 = number(from: array1)
	let num2 = number(from: array2)
	let sum = num1 + num2
	return array(from: sum)

That’s clear, right? There are two functions referenced in the above code that are clearly transformers — one goes from an array to a number, and the other goes from a number to an array.

So the next steps are to fill those in, along with any additional helper functions.

If I were on the other side of the table, and this is what the candidate did, I would be quite happy — because they’ve achieved not just correctness but *clarity*. They’ve solved the problem using a coding style that I’d want to see in production code.

*But that’s not what these questions want to see at all.*

#### What the Questions Actually Want

What they want — at least in the experience I’ve had so far — is for you to have some kind of insight into the problem that allows you to solve it in a more efficient way.

You may have already figured it out for this particular question: but, just in case not, here’s the tip — the answer should mirror the way we actually do sums on paper.

Remember that we go right-to-left, and we build up the answer digit-by-digit.

	   624
	+ 8083
	------
	  8707

The arrays are already backward, even! So just write a loop that does exactly what you do when doing this by hand (including the carry-the-one part). You create the answer — the `[7,0,7,8]` — as you go along.

#### I’m Not Sure What to Think About This

In production code, if a problem like this came up, I’d ask “How the hell did we get here?” and try to backtrack and figure out what insanity caused this, because it’s just not right.

But, if this code were truly needed, I’d write code the way I normally would, with clarity in mind first.

And then, if my tools told me it was too inefficient with time or space, I’d figure out a more efficient version.

These questions, then, are able to test what you might come up with when you’re in that position.

The thing is, what I would most want to know is how people write code for the 99% of time when they’re *not* in that position. That’s not being tested here.
