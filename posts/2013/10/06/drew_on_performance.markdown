@title Drew on Performance
@pubDate Sun Oct 06 14:28:24 -0700 2013
@modDate Sun Oct 06 14:29:03 -0700 2013
Responding to my <a href="/2013/10/05/why_care_about_30_000_notes_">previous post</a> on performance, Drew McCormack writes <a href="http://mentalfaculty.tumblr.com/post/63291176713/theres-no-free-lunch-when-it-comes-to-performance-or">There’s No Free Lunch When it Comes to Performance (Or Anything Else for that Matter)</a>:

>In my view, Brent has this all backwards. He is thinking up a mythical user with 30000 Vesper notes, and wants to be sure that that 1/1000th of a percent of his customers doesn’t experience any lag. What he doesn’t seem to realize, is that that choice has a big impact on the other 99.999% of his costumers, who almost certainly will pay a performance penalty.

I would have expected it would go without saying that the 99% or 99.999% come first. Performance has to be awesome for them, and I would never accept a trade-off where it got worse for most people just so it could be acceptable for the very few.

Drew also writes:

>See, there’s no such thing as a free lunch in the performance game. It’s a mathematical fact. You can even read about it on <a href="http://en.wikipedia.org/wiki/No_free_lunch_theorem">Wikipedia</a>. When you optimize a program for one scenario, you are making it less optimal for other scenarios.

Drew is absolutely correct that there’s no free lunch. There are always trade-offs.

However, there’s a trade-off Drew didn’t appear to consider: you can often beat the performance of a general system like Core Data — for <em>both</em> the 99% and the 1% — by creating a custom, hand-tuned system.

The trade-off means that it’s more code and more work for the developer, but the app performs better for 100% of users.

The question, then, is whether or not that particular trade-off is worth it, which must be answered on a case-by-case basis, which often requires actual measurement.

PS You should check out Drew’s project <a href="http://mentalfaculty.tumblr.com/post/62909673342/introducing-ensembles-core-data-sync-the-way-it-should">Ensembles</a>, a new Core Data sync framework. Interesting for sure, and could turn into something quite valuable.
