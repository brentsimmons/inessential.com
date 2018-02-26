@title Imagining a Scripting Language
@pubDate 2014-03-11 17:45:48 -0700
@modDate 2014-03-11 20:18:54 -0700
My [earlier post](http://inessential.com/2014/03/11/strange_dialect) about WebScript and JSTalk got me thinking: what if I could write part of my app using a scripting language?

First let’s imagine a language: Shasta, named for the mountain in California. It works with Objective-C — in fact, its objects are Objective-C objects, and Objective-C objects are Shasta objects. You can, for instance, subclass UIViewController. The Cocoa APIs are almost all available to Shasta.

It has blocks, because otherwise we wouldn't use it.

You can use the language on a file-by-file basis, kind of like how can turn ARC on/off per file.

Another thing: it’s interpreted. The code itself is included with the app. Anyone can look in the bundle and see the code.

And because it’s a scripting language, you can’t use C. There would probably have to be replacements for common things (like for loops, GCD, and enums) and they may be syntax-compatible with C. (And maybe not.) But there’s no C in Shasta.

Let’s assume it’s fun to write Shasta code and it makes some things easier. Block syntax is simpler, and perhaps there’s never a need to declare `__block` variables and do things like the weakself dance. Imagine whatever syntax you like that’s easy to read, easy to write, and expressive. 

Let’s also assume it works with the debugger, auto-complete, static analysis, Instruments, and all the tools we’re used to.

Would I use this in my app?

Consider that I’d still use Objective-C when needed. But there’s a whole bunch of code that could just as well be done in a scripting language. And perhaps be done better and faster — perhaps it would make for better apps that are easier to develop.

The rub, it appears to me, in this scenario, is that the actual code is included in the app’s bundle.

One way around it would be to pre-compile the scripts to bytecode. But let’s assume that’s not available. Still worth it?

Yes. (For this imaginary language, at least.)

In thinking about this, I realized that most of the code in my app — in almost any app — is *just some code*. Some view controllers doing their things. Animations. Layout. Action methods. Caches. Web views.

If that’s true, then why not make our apps open source?

Well, we’re not going to. But I can’t help but wonder what it would be like if developers — even developers of for-pay apps — routinely made their apps open source. (Perhaps with a license that says you can’t just re-skin it and sell it as your own.)

People would still buy the apps.

But I stop there, at wondering. I’m not advocating anything — just thinking about what would happen. It could be interesting. But it sounds scary.

<i>Update 8:15 pm</i>: People have mentioned [nu](http://programming.nu/) and [RubyMotion](http://www.rubymotion.com/) and others. And those are cool, no doubt, and I’m tempted to take a closer look.

However, what I’d really want is a peer of Objective-C — that is, something that works with Xcode’s debugger and Instruments just as well as Objective-C. It would also allow me to mix Objective-C and scripting language files.

But, more importantly, this post (despite the title) isn’t really about a scripting language. That just provided me a way to ask the question: <em>why not make our apps open source?</em> (No matter what language they’re written in.)

Partly it’s just because it’s extra work. Partly it’s the fear that people will run the open source version rather than buy our app. Partly it’s the fear that someone else will rip off our code and easily make a competing app.

I wonder if the fears are overblown. I wonder — just *wonder*, not state — if we’re not missing out on a good idea.
