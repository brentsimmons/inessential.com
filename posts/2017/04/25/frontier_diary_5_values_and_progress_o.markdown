@title Frontier Diary #5: Values and Progress on the Language
@pubDate 2017-04-25 13:26:33 -0700
@modDate 2017-04-25 13:41:26 -0700
I put the <a href="https://github.com/brentsimmons/Frontier">Frontier repository</a> up on GitHub.

(The build is currently broken. This is bad discipline, but since it’s still just me, I forgive myself. Sometimes I run out of time and I just commit what I have.)

The repo has my new code and it also contains <a href="https://github.com/brentsimmons/Frontier/tree/master/FrontierOrigFork">FrontierOrigFork</a>, which is the original Frontier source with a bunch of deletions and some changes. The point is to give me 1) code to read and 2) a project that builds and runs on <a href="http://inessential.com/2017/04/03/frontier_diary_1_vm_life">my 10.6.8 virtual machine</a>.

The original code is in C, and the port is, at least so far, all in Swift. In the end it should be *almost* all in Swift, but I anticipate a couple places where I may need to use Objective-C.

Here’s one of the Swift wins:

#### Values

Since Frontier contains a database and scripting language, there’s a need for some kind of value object that could be a boolean, integer, string, date, and so on.

Original Frontier used a <a href="https://github.com/brentsimmons/Frontier/blob/master/FrontierOrigFork/Common/headers/lang.h">tyvaluedata</a> union, with fields for the various types of values.

This is a perfectly reasonably approach in C. It’s great because you can pass the same type of value object everywhere.

Were I writing this in Objective-C, however, I’d create a `Value` protocol, and then create new value objects for some types and also extend existing objects (`NSNumber`, `NSString`, etc.) to conform to the `Value` protocol. This would still give me the upside — passing a `Value` type everywhere — while reducing the amount of boxing.

But: this still means I have an `NSNumber` when I really want a BOOL. Luckily, in Swift I can go one better: I can extend types such as <a href="https://github.com/brentsimmons/Frontier/blob/master/FrontierData/FrontierData/Value/ValueBool.swift">Bool</a> and `Int` to conform to a <a href="https://github.com/brentsimmons/Frontier/blob/master/FrontierData/FrontierData/Value/ValueProtocol.swift">Value</a> protocol.

This means passing around an *actual* `Bool` rather than a boxed boolean. I like this a ton. It feels totally right.

Other topic:

#### Language Progress

I’m still in architectural mode, where I’m writing just enough code to validate and refine my decisions. A couple days ago I started on the <a href="https://github.com/brentsimmons/Frontier/blob/master/UserTalk/UserTalk/LangEvaluator.swift">language evaluator</a> — the thing that actually runs scripts.

It works as you expect: it takes a compiled code tree and recursively evaluates it. It’s not difficult — it’s just that it’s going to end up being a fair amount of code.

I’ve done just enough to know that I’m on the right path. (The Swift code looks a lot like the C code in OrigFrontier’s <a href="https://github.com/brentsimmons/Frontier/blob/master/FrontierOrigFork/Common/source/langevaluate.c">langevaluate.c</a>. See `evaluateList`, for instance.)

The next step is for me to build the parser. I thought about writing a parser by hand, because it sounds like fun, and it would give me some extra control — but, really, it would slow me way down, so forget it.

OrigFrontier generated its parser by passing a grammar file — <a href="https://github.com/brentsimmons/Frontier/blob/master/FrontierOrigFork/Common/source/langparser.y">langparser.y</a> — to MacYacc (there was such a thing!), which generated <a href="https://github.com/brentsimmons/Frontier/blob/master/FrontierOrigFork/Common/source/langparser.c">langparser.c</a>.

I’ll do a similar thing, except using <a href="https://www.gnu.org/software/bison/">Bison</a> (which is compatible with Yacc). Or, possibly, using the <a href="http://www.hwaci.com/sw/lemon/">Lemon parser generator</a> instead. Either way, I’ll want the generated code to be Objective-C. (Well, mostly C, but with Objective-C objects instead of structs.) (I don’t know of a generator that would create Swift code.)

This is completely new territory for me, and is exciting.

(Almost forgot to mention: I’ll need to write a tokenizer. This means porting <a href="https://github.com/brentsimmons/Frontier/blob/master/FrontierOrigFork/Common/source/langscan.c">langscan.c</a>. I’ll need to do this first, since the parser generator needs it. So this is the real next step.)
