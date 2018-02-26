@title Mark on What’s Really Dangerous
@pubDate 2014-04-13 12:03:30 -0700
@modDate 2014-04-13 12:03:30 -0700
Mark Bernstein: [It’s Not C](http://www.markbernstein.org/Apr14/ItsNotC.html).

><em>Any</em> computer language capable of doing real work is also capable of being confusing, capable of being misused, capable of being subverted.

Mark’s right. Free computing is free speech.

I certainly don’t recommend banning C, as if anyone could. I don’t use it much, but when performance is an issue, [I do](https://github.com/quartermaster/QSKit/blob/master/Classes/Foundation/QSDateParser.m). (Note that I need to update that code: needs more braces.)

However, it’s worth thinking about less-dangerous alternatives. Programmers will always make mistakes, and that’s why we do automated testing, static analysis, code reviews, and so on. That same reason — the inevitability of mistakes — is a reason to use higher-level languages when possible.

Unfortunately, “when possible” is just not very often when it comes to portable libraries such as OpenSSL. What *would* you write it in, if not C? I don’t know, but I think it makes sense to have an alternative language for this where you don’t have to be so damn careful with memory, where things like buffer over-runs are impossible.

I suppose that static analysis tools could get good enough to catch these errors. Maybe. C is so flexible that I just don’t know if they’ll ever be good enough. But if they get that good, then the culture and the tools have to make it so that no developer would ever fail to run and pay attention to static analysis results. That seems like a longshot to me, but I’d be pleased to be wrong.

An even bigger longshot is counting on developers to get better at testing. That’s like counting on people not to drink and drive. The culture has done a good job at stigmatizing this particular bad idea — but it still happens. That’s not to say we shouldn’t try — we should, definitely, for sure — but alone it’s not enough to fix the problem.

Though the OpenSSL bug affected servers, I note that most people don’t write their web services and sites in C. It’s do-able. You *could*, and surely some people are, somewhere. But to most of us it sounds crazy, and for good reason.

As computing evolves, the domains where C “sounds crazy” will continue to expand. Consider that people are already treating *JavaScript* as assembler (see [CoffeeScript](http://coffeescript.org/) and [TypeScript](http://www.typescriptlang.org/)). As an industry we continue to move toward higher-level languages, and that’s a good thing.
