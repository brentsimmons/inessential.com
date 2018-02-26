@title Oldie Praises the Old Old Ways
@pubDate 2016-06-01 13:56:11 -0700
@modDate 2016-06-01 14:06:56 -0700
Swift’s support of inner functions is one of my favorite features of the language.

Years ago, back in the ’90s, I used to write in UserTalk, the language that powered UserLand Frontier. It was a procedural scripting language — but remarkable for its integration with Frontier’s hierarchical, persistent database. (Storing a string in the database, for example, was just a matter of assigning to a location: `foo.bar = "baz"`.)

In the early days of web programming, we’d often build a page just by appending to a string. In UserTalk it looked something like this:

<code>on buildPage()</code><br />
<code>&nbsp;&nbsp;local (htmlText)</code><br />
<code>&nbsp;&nbsp;on add(s)</code><br />
<code>&nbsp;&nbsp;&nbsp;&nbsp;htmlText = htmlText + s + "\n"</code><br />
<code>&nbsp;&nbsp;add("&lt;html>")</code><br />
<code>&nbsp;&nbsp;add("&lt;head>")</code><br />
<code>&nbsp;&nbsp;// …build the rest of the page…</code><br />
<code>&nbsp;&nbsp;add("&lt;/body>&lt;/html>")</code><br />
<code>&nbsp;&nbsp;return htmlText</code>

The `on add(s)` bit was the inner function, and it could refer to variables in its enclosing scope.

That’s a simple example, of course — we did more with this feature than just appending to strings, but it gets the idea across.

#### Objective-C

Before we get to Swift, let’s start where I started, with Objective-C.

Some time last year I wrote a macro processor. The API looked something like this:

<code>@interface MacroProcessor : NSObject</code>

<code>- (instancetype)initWithText:(NSString \*)text values:(NSDictionary \*)d;</code><br />
<code>@property (nonatomic, readonly) NSString *processedText;</code>

<code>@end</code>

That’s not an uncommon pattern. Initialize an object with some input, and then get the result (via the readonly `processedText` property).

I’d call it like this:

<code>MacroProcessor \*macroProcessor = [[MacroProcessor alloc] initWithText:text values:values];</code><br />
<code>NSString \*processedText = macroProcessor.processedText;</code>

It sure just looks like a function call at that point, right? But weirdly split up into two lines.

So I added a C function to the API to make this more explicit:

<code>TextWithMacrosProcessed(NSString \*text, NSDictionary \*values);</code>

Now I could call it like this, instead:

<code>NSString \*processedText = TextWithMacrosProcessed(text, values);</code>

That C function just wrapped up the two lines (alloc-init MacroProcessor and return `processedText`).

(I could have, alternately, made a class method on MacroProcessor. Either way’s fine.)

Then I thought: well, I have the API I want — a function call — so there’s no need to make `initWithText` and `processedText` public, so I removed everything but that C function from the .h file. Great. Fine.

That’s the beauty of interfaces, right? The important part is to get the API right. How it works under the hood (creating an object, etc.) is an implementation detail.

I could have stopped there.

#### But I didn’t stop there

Let’s be clear: MacroProcessor had unit tests and zero known bugs. It had no side effects. It was good, solid code. A smart developer just moves on to work on something else.

But, since this was part of a Ranchero project (not an Omni app) with no ship date and no hurry, I could allow myself some extra time.

Even though I had the API right, it bothered me that the implementation didn’t feel quite right. After all, if the API is a function, wouldn’t it be ideal if the implementation was also a function?

Is that even possible? I looked at the structure of MacroProcessor, and it was what you’d expect: three properties (initialText, values, and processedText) and a handful of methods.

For some reason it flashed in my head how I’d do this in the old days, back when I was writing UserTalk. There’d be a function with some local variables, and some inner functions that did things, and it would return the final processed text. Like that `buildPage` example above.

And it occurred to me that the structure is actually the same: some functions have access to variables that nobody else has access to. Whether that’s an object, or it’s a function with variables and inner functions, *amounts to the same thing*.

So I approached it that way, and wrote it like I would have in the old days (only in Swift this time), and it worked perfectly. (Still has unit tests, zero known bugs, and no side effects.)

And the API is now <code>textWith&#8203;Macros&#8203;Processed&#8203;(text: String, values: [String: String]) -> String</code>, and the entire thing is just that one function. *No object needed*.

#### Good old days, bad old days

So one day I talk about how I don’t want to write code like I did in the <a href="http://inessential.com/2016/05/25/oldie_complains_about_the_old_old_ways">old days</a>. And today I’m *happy* because I’m writing code like the old days.

There’s no contradiction. Some stuff from the old days was awesome, and some was fine, and some was bad. Writing Swift this way to do something that I’d solve with an object in Objective-C — at least in the case where it really ought to be a pure function (takes input, does a thing, doesn’t look at or change anything else, returns output) — is *great*. Love it.

(Pure functions make me unreasonably excited. I think I get this from my Mom.)
