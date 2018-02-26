@title Vesper Sync Diary #4 - In Another Country
@pubDate 2013-11-07 16:01:58 -0800
@modDate 2013-11-09 10:51:38 -0800
I mentioned previously that Vesper will [sync via web services](http://inessential.com/2013/11/05/vesper_sync_diary_3_immutability_del).

Web services don’t just appear out of the foam like Aphrodite from the sea — they have to be written. Though I was tempted to run a server on a Mac and write the backend in Objective-C, I decided to do what normal people do: use a scripting language. JavaScript.

Here are the main features of JavaScript country — what I’ve seen so far, anyway. (You may know all this already. If so, skip it. This is written for people like me who are mainly Cocoa developers.)

#### Node.js

It’s a [fast JavaScript runtime, library, and server](http://nodejs.org/). It’s interesting in that it doesn’t create a bunch of threads: instead, [it uses callbacks](http://nodejs.org/about/). Once you get over the shock of a different language, it should seem very familiar to Cocoa developers.

Now, of course, there are two ways of doing callbacks, and there’s only one way that’s bearable: closures. (Blocks, in Objective-C-world.) [JavaScript has closures](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Closures). I had no idea.

(Before I got started, I thought of JavaScript as the web’s answer to AppleScript — hard to write and prickly, seemingly nondeterministic. I’m getting over that.)

#### Learning JavaScript

Node.js comes with a REPL, which is great when trying to get the hang of the syntax and libraries. Here’s an example pasted from Terminal:

<code>> d = {foo : "bar"}</code><br />
<code>{ foo: 'bar' }</code><br />
<code>> d.foo</code><br />
<code>'bar'</code><br />
<code>> d['foo']</code><br />
<code>'bar'</code><br />
<code>> d[foo]</code><br />
<code>ReferenceError: foo is not defined</code><br />
<code>&nbsp;&nbsp;at repl:1:4</code><br />
<code>&nbsp;&nbsp;at REPLServer.self.eval (repl.js:109:21)</code><br />
<code>&nbsp;&nbsp;at Interface.&lt;anonymous> (repl.js:248:12)</code><br />
<code>&nbsp;&nbsp;at Interface.EventEmitter.emit (events.js:96:17)</code><br />
<code>&nbsp;&nbsp;at Interface._onLine (readline.js:200:10)</code><br />
<code>&nbsp;&nbsp;at Interface._line (readline.js:518:8)</code><br />
<code>&nbsp;&nbsp;at Interface._ttyWrite (readline.js:736:14)</code><br />
<code>&nbsp;&nbsp;at ReadStream.onkeypress (readline.js:97:10)</code><br />
<code>&nbsp;&nbsp;at ReadStream.EventEmitter.emit (events.js:126:20)</code><br />
<code>&nbsp;&nbsp;at emitKey (readline.js:1058:12)</code>

This examples illustrates one of the parts of JavaScript I find weird. You can create a dictionary like this: <code>{foo : 'bar'}</code> where `foo` isn’t a defined variable.

And then you can refer to `d.foo` and `d['foo']` but *not* to `d[foo]`.

What happens if foo *is* a defined variable?

<code>> foo = "xyz"</code><br />
<code>'xyz'</code><br />
<code>> d = {foo : "bar"}</code><br />
<code>{ foo: 'bar' }</code>

This makes me nervous.

Another weird thing is `===`, which bypasses type coercion. `x === y` means that x and y are equal *and* the same type. (Most of the time you probably want `===`, for safety’s sake.)

A third weird thing: `const` is not yet part of the official language. (Though some implementations have added it.) This freaks me out.

There’s plenty to like about JavaScript, and I do like it. It certainly saves typing (compared to Objective-C; but then, what doesn’t?). Everything is a var. Function parameters are untyped. It has the usual advantages of scripting languages (which are also the usual disadvantages).

JavaScript is not just for server-side work (or in-the-browser work). You can [write shell scripts in JavaScript](http://www.2ality.com/2011/12/nodejs-shell-scripting.html) via Node.js.

You can even script Mac apps and do Cocoa-ish things — see Gus’s [JSTalk](http://jstalk.org/).

#### Mocha

I recently spent a few days adding unit tests to Vesper. (It would take another week to get caught-up.) Even though some things are hard or impossible to test — does that animation look right? — it’s still worth it for the low-level code. (It’s so much easier to concentrate on that awesome animation code if you know the app’s foundation is solid and bug-free.)

The good thing about server-side JavaScript is that, in theory, it’s all testable. It’s all low-level code: no UI, no animations, nothing the user actually sees.

I’m using [Mocha](http://visionmedia.github.io/mocha/) for testing. It’s easy.

One of the frustrations with XCTest is that you have to do special things (run the runloop) to handle asynchronous tests. (I haven’t even tried yet.) Mocha handles asynchronous tests easily.

It even provides color-coded output, which I like.

#### Text Editors

I live in Xcode, like most Cocoa developers. My editor for everything else is [BBEdit](http://www.barebones.com/products/bbedit/).

But last night I wondered if there might be another editor that’s particularly stellar for JavaScript development. I tried three.

[Sublime Text](http://www.sublimetext.com/) lasted about a minute. It appears to be wonderfully powerful — but it’s also not Mac-like. The first thing I did was open a file and select some text. Dead give-away right there. Then I checked out the preferences. Ah. No. Not for me, though I appreciate that many people love it.

[TextMate 2 alpha](http://macromates.com/download) is a Mac app. But there were deal-stoppers there too. (Deal-stoppers for me. This is *all* personal taste.) I didn’t like having to double-click in the file list to open a file. I especially didn’t like that I couldn’t find an easy way to edit the color schemes. (I like syntax coloring, but can’t stand syntax-bolding and syntax-italicizing.)

I like [Chocolat](https://chocolatapp.com/). It’s very much a Mac app. The file list works via single-click. I could turn off syntax-bolding and syntax-italicizing. It has some nice features, too — my favorite so far is the always-visible symbols list.

Chocolat also looks better than the other text editors. It’s cleaner. (It’s weird to care about that, since I’m mostly just looking at *text*. But it means the app has fewer things to distract from the text.)

Chocolat isn’t without issues, though, and I have 14 days left to decide whether or not to buy it. (It’s $49, a totally fair price for a development tool.)

*Update a few minutes later.* Matthew Johnson has TextMate tips: [how to change the bold/italics](https://twitter.com/anandabits/status/398609652989976576) and [how to open a file with a single click](https://twitter.com/anandabits/status/398609262777098240).

*Update quite a few minutes later.* I forgot to mention that I’m also using [Express](http://expressjs.com/). Don’t use Node without it.

*Update a couple days later.* I tried Chocolat for a while, then tried TextMate 2 for a while — then went back to BBEdit.
