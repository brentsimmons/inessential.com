@title How Not to Crash #9: Mindset
@pubDate 2015-06-10 16:05:32 -0700
@modDate 2015-06-10 16:26:19 -0700
You know the old line about not writing code that’s as clever as you are, because it will take someone even <em>smarter</em> than you to debug it?

I used to think that means I should write code that’s about 80% as clever as I am. Save a little bit for debugging.

But over the years I’ve come to think that I should write code that’s about 10% as clever as I am. And I’ve come to believe that true cleverness is in making code so clear and obvious that it looks like nothing at all.

And that’s why I have rules like <em><a href="http://inessential.com/2015/05/22/how_not_to_crash_4_threading">do everything on the main thread except for perfectly isolatable things</a></em> and <em><a href="http://inessential.com/2015/05/27/how_not_to_crash_6_properties_and_acce">avoid unsafe_unretained always</a></em> and so on.

This means I don’t get bonus points for being a code magician. I don’t pull rabbits out of hats and I certainly don’t walk tightropes. I won’t even <em>look</em> at tightropes.

I do difficult things as needed, but the goal even with the difficult things is to write the simplest and most-readable code that I can. If, in the end, the code looks easy — unimpressive, even, as if a middle-school kid could have written it — then *good*.

In the small, this means that methods tend to be small and focused with little nesting. In the large, architecture and naming is iterated-over until it feels inevitable, as if no thought went into it because it all must have been obvious.

It means not getting too abstract. Explicitness is obviousness. But it also means not getting too non-general, either — there are times when two or three things are really the same thing, and they can be generalized without harming maintainability. (And there are times when they can’t.)

I avoid tight coupling and large structures — except for when the best solution really is for x to know about y.

And I keep learning and getting better.

#### Time

The thing that separates programming from painting, writing, architecture, and composing music is that there is no finished product. There are released versions, yes, but there’s no finishing, there’s only abandoning.

Code exists in time, and maybe across many people — and you don’t even know how long or who. This should never be out of your mind.

#### Cape, mask

When I was younger I wanted to be a code magician — or, really, a <em>hero</em>. But I learned that <em>actual software quality is more important than what I imagine other people think of me</em>.

And, more: quality is a reward that’s almost spiritual. It’s an act of devotion, both selfish and unselfish, to something more important than ego.

Selfish because the process of striving for quality makes you a better person. And unselfish because better code and better software is better for other people.

And the first thing other people ask of your software is that, if they launch it, it *stays* launched. Any programmer who can’t bring themselves to care about that — or who rationalizes away crashing as a fact of life these days — isn’t taking this great fun we are privileged to have seriously enough.
