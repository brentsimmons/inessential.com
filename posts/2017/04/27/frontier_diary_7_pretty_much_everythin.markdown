@title Frontier Diary #7: Pretty Much Everything Throws
@pubDate 2017-04-27 13:30:42 -0700
@modDate 2017-04-27 13:48:09 -0700
A script can throw an error, either intentionally (via the `scriptError` verb) or by doing something, such as referencing an undefined object, that generates an error.

OrigFrontier was written in C, which has no error-throwing mechanism, and so it worked like this: most runtime functions returned a boolean (for success or failure), and the return value was passed in by reference. If there was an error, the function would set a global error variable and return false. The caller would then have to check that global to see if there was an error, and then do the right thing.

This was not unreasonable, given the language and the times (early ’90s) and also given the need to be very careful about unwinding memory allocations.

But, these days, it seems to me that Swift’s error system is the way to go. There’s just one downside to that, and it’s that I have to do that do/try/catch dance all over the place, since pretty much any runtime function can throw an error.

Even the coercions can throw, so last night I changed the <a href="https://github.com/brentsimmons/Frontier/blob/master/FrontierData/FrontierData/Value/ValueProtocol.swift">Value</a> protocol so that `asInt` and so on are now functions, since properties can’t throw (at least not yet).

The extra housekeeping — the do/try/catch stuff — kind of bugs me, but it’s honest. I considered making script errors just another type of Value — but that meant that all those callers have to check the returned Value to see if it’s an error, and then do the right thing. Better to just use Swift’s error system, because it makes for more consistent code, and it makes sure I’m catching errors in every case.

It also means I’m not multiplying entities. A Swift error is a script error, and vice versa.

<p style="text-align:center">* * *</p>

Working on this code is like applying the last 25 years of programming history all at once.

A completely different type of error is a *bug*, and I’m certain to write a bunch of them, because that’s how programming goes.

That’s where unit tests come in. Frontier has long had a stress-test suite of scripts — you’d launch the app, run that suite, wait a while, and see if there are any errors. This was critically helpful.

But OrigFontier didn’t have unit tests at the C code level. The new version does. (Well, <a href="https://github.com/brentsimmons/Frontier/blob/master/FrontierVerbs/FrontierVerbsTests/Math.swift">I’ve started them anyway</a>.) This means I can more easily follow <a href="http://scripting.com/2002/09/29.html#rule1">Rule 1</a> — the no-breakage rule — and can also more easily follow Rule 1b — the don’t-break-Dave rule.

PS I’ve added a <a href="http://inessential.com/frontierdiary">collection page for the Frontier Diary</a>, as I did with earlier diaries. There’s a link to it in the footer of every page on the blog.
