@title Random Swift Things
@pubDate 2015-02-04 11:37:52 -0800
@modDate 2015-02-04 12:11:38 -0800
Last night I discussed Swift with some local developers. Some of it stuck in my head today. At random:

#### Question

It’s two years from now. Your company is hiring, and the best candidate has one drawback: all her experience is with Swift, and she’s barely acquainted with Objective-C. But she knows the frameworks well and has proven experience shipping quality software.

All of your existing code — and there’s a ton of it — is in Objective-C. Maybe there’s a little bit in Swift, maybe not, and maybe you’re open to doing more in Swift, and maybe not.

Do you hire this person?

#### Swift Is Hard

Objective-C looks hard because of the [ and ] syntax and all those words. It looks kind of *mean*, actually, like an angry grandpa with bushy eyebrows who makes you spell out “I am laughing out loud” instead of writing LOL.

But Objective-C is easy compared to Swift. Swift *looks* easier at first blush — every JavaScript developer sees it as familiar, and many think that this might be their way in to writing native apps.

More-familiar syntax will help more people get started, I think. But then you run into concepts that Objective-C doesn’t have to deal with (optionals, generics, and tuples, for instance) and concepts that Objective-C doesn’t have to deal with much (value versus reference semantics, functional design patterns, strict type safety). And you inevitably run into the issue of interoperation with Objective-C — which, obviously, isn’t a problem in Objective-C.

#### Angle-bracket-T Blindness

I’ll exaggerate a little — okay, a lot — to make a point. A popular form of blog post about Swift seems to be like this:

>Here’s how you’d do things the crufty old-fashioned way:
>
><code>for (id oneObject in someCollection) {</code><br />
><code>&nbsp;&nbsp;[self doSomethingWithObject:oneObject];</code><br />
><code>&nbsp;&nbsp;}</code>
>
>Well, you can tell by looking just how awful this is. Nasty loopses and untyped types. Let’s do it the modern way…
>
>[snip]
>
>[snip 200 lines of code]
>
><code>func x&lt;T> -> x&lt;U> &lt;TT> (in U -> &lt;T>){$1 $2}.map(func y(T)&lt;T>&lt;T> -> &lt;U> infix $3 {</code>

Clearly this is hyperbole and ridiculousness and line noise. I’m not being fair. But I think that anybody who reads a bunch of articles about Swift (as I do: I read everything I can find) recognizes what I’m talking about.

(There are many people who write wonderfully about Swift. Two of my favorites are <a href="http://nshipster.com/">NSHipster</a> and <a href="http://owensd.io/">David Owens II</a>. But I still get angle-bracket-T blindness sometimes, even with them.)

#### Objective-C Hasn’t Finished Evolving

This is a prediction. It’s surely true that Apple has more existing Objective-C code than anyone else in the world. Improving Objective-C — especially if it means making their developers more productive and making their apps better — is in Apple’s best interest.

It’s possible we’ll even see some convergences — changes to Objective-C that make it easier for Objective-C and Swift to work together in the same code base.

I keep thinking it’s easier for Apple to upgrade Objective-C than to redo everything in Swift.

#### But Swift Is the Future

Swift’s adoption, and the enthusiasm around it, have surpassed my expectations — despite its very-much-still-early position. (If you have a developer account, read <a href="https://devforums.apple.com/community/tools/languages/swift">Apple’s Swift forum</a>.)

Here’s the thing: if you go searching the web for solutions to some problem involving recent APIs, you’re extremely likely to run into Swift code. It’s happened to me plenty of times already — I’m translating from Swift to Objective-C as I read, which is not something I expected so soon.

<em>Swift is happening.</em>

#### P.S.

Yes, I’d hire the person with Swift experience but no Objective-C experience.
