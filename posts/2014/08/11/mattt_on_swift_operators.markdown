@title Mattt on Swift Operators
@pubDate 2014-08-11 11:20:24 -0700
@modDate 2014-08-11 11:20:24 -0700
Mattt Thompson, in <a href="http://nshipster.com/swift-operators/">Swift Operators</a>, talks about overloading operators and proposes some guidelines.

He provides some examples that seem reasonable. <code>2 \*\* 3</code> could mean two-to-the-third-power, for instance.

Or <code>=~</code> could mean is-regex-matchable. Or <code>√4</code> could take the square root of 4.

I wasn’t a C++ developer and I don’t have any horror stories — and yet I’m still <em>extremely</em> wary of custom operators and operator overloading.

One of the great things about Cocoa and Objective-C is how easy it is to read other people’s code. If we’re both following the conventions and standard patterns, your code looks much like mine. This blows that up.

There’s an argument against every example I’ve seen so far (in this article and elsewhere). One or more of the following seems to apply in every case:

* You can’t type the thing without copy-and-paste. (The √ character, for instance.)

* You don’t know what it means without looking it up. (The \*\* and =~ examples.) Function <em>names are easier to read than symbols</em>, even mathematical symbols (except in the most common cases, which are already part of the language).

* You lose out on auto-complete that you get when you use functions like pow, sqrt, and match instead of operators. Operators are thus often *less* convenient than functions.

Mattt’s guidelines are pretty good — especially “Don't create an operator unless its meaning is obvious and undisputed.” I’d argue that one only of his examples (√) is obvious and undisputed, and it suffers from the copy/paste problem. (It’s *way* easier to type <code>sqrt</code>, especially with auto-complete.)

Brent’s guidelines on custom operators and operator overloading would be simple and short: don’t use them.

Maybe in a year or two we’ll nominate someone suitably diligent — <a href="http://www.manton.org">Manton Reece</a>, perhaps — to try a custom operator in his code. We’ll ask him to report monthly on his health and well-being, and after another year — if he hasn’t ripped it out of his code, if he isn’t suffering from any ill effects (blurred vision, headaches, joint pain) — we’ll ask him to post it as a gist so we can see it.

Then let’s take another year to decide who can go next. After a decade or two we’ll have an idea whether or not cautious, limited use of custom operators is okay in some rare situations.

(You think I’m exaggerating.)
