@title Changed My Mind on This One Thing With Braces
@pubDate 2013-10-24 14:23:53 -0700
@modDate 2013-10-24 14:23:53 -0700
I’ve always written my `if` statements like this:

<code>if (something)</code><br />
<code>&nbsp;&nbsp;doAThing();</code><br />

That is — no braces when the code under the `if` is just one line.

That’s never, not even once, been a problem for me. Never caused a bug.

And, as a relentless cutter, a simplifier by temperament, I like it because it means I can do without a couple braces. Though it doesn’t make a difference to the generated code, it does means less actual characters in the source file, and it saves a line for the closing brace.

But I recently changed my mind. Now I write it like this:

<code>if (something) {</code><br />
<code>&nbsp;&nbsp;doAThing();</code><br />
<code>&nbsp;&nbsp;}</code><br />

And for the same reason: for the reason of simplification.

It’s simpler because it removes a special case, which means I no longer have to notice that it’s one line or multiple lines and add or delete braces as needed. I’ve simplified what my brain has to do at the cost of some more braces in the source code. I can live with that trade-off.

(Second reason: it’s likely that I was the last Cocoa coder to omit the braces on these statements, and I’ve learned [the](http://www.taplynx.com/) [hard](http://netnewswireapp.com/) [way](http://www.red-sweater.com/marsedit/) that other people are going to work on my code some day. Even with Vesper we’ve had [Doug Russell](http://www.takingnotes.co/) work on the code, on accessibility.)

PS But you know what I’m never going to do? Write methods like this:

<code>- (void)doSomething</code><br />
<code>{</code><br />
<code>&nbsp;&nbsp;doAThing();</code><br />
<code>}</code><br />

I absolutely *cannot bear* that extra line for the opening brace. It gives me gas. I’ll often — usually, even — put a blank line there, but a blank line is nice and clean. A line with just an opening brace is like a fingernail on the page. (And it ruins the clean left edge of - to open and } to close.) Instead I’d write it like this:

<code>- (void)doSomething {</code><br />
<code></code><br />
<code>&nbsp;&nbsp;doAThing();</code><br />
<code>}</code><br />

PPS Reasonable people may disagree. It’s a cinch that unreasonable people will also disagree.
