@title How to Solve Tabs vs. Spaces Forever
@pubDate 2015-12-21 12:09:13 -0800
@modDate 2015-12-22 11:29:32 -0800
Code is a tree structure, but we use text editors to write and edit code.

Picture this bit of Swift:

<code>if let x = foo() {</code><br />
<code>&nbsp;&nbsp;&nbsp;&nbsp;bar(x)</code><br />
<code>&nbsp;&nbsp;&nbsp;&nbsp;moreThings(x)</code><br />
<code>}</code><br />
<code>someOtherCode()</code>

The braces are there to make the structure explicit, and the indentation is there for human-readability. Picture this same bit of Swift written using a tree structure editor — an outliner:

<code>if let x = foo()</code><br />
<code>&nbsp;&nbsp;&nbsp;&nbsp;bar(x)</code><br />
<code>&nbsp;&nbsp;&nbsp;&nbsp;moreThings(x)</code><br />
<code>someOtherCode()</code>

No braces needed. You can’t see it in the example above, but the indentation isn’t tabs or spaces — it’s part of the UI of the outliner.

You also can’t see how easy it is rearrange code. To move the entire <code>if let…</code> section, you’d grab that line and move it (via mouse or keyboard), and the entire block of code (before <code>someOtherCode()</code>) would go with it.

You can also expand and collapse things to get a high-level view, and drill down into detail when needed. (Code folding gives you some of this, but it’s always been a poor substitute for an actual outliner.)

<p style="text-align:center">* * *</p>

One of the arguments against using an outliner to edit code is that code wouldn’t be in a plain-text format, and it’s wise to store things like code in a plain-text format.

Well, it’s easy enough to translate plain-text code to an outline and back. The plain-text format would include braces, and it would use tabs or spaces (whichever) for indentation.

You could still use your favorite SCM and diff tools and everything else with that code. You could still collaborate with people who prefer a text editor.

<p style="text-align:center">* * *</p>

Another possible argument against using an outliner is that nobody’s ever tried it, and so we don’t know how horrible it would be in practice.

This argument isn’t true. I wrote most of my code in an outliner for eight years (when I was working on UserLand Frontier). And I miss it every day. Writing code in an outliner is the exact opposite of horrible. It’s *marvelous*.

I wish Xcode had an outline mode.

PS These days I work on OmniOutliner for Mac. Because I learned to love outliners from writing code in an outliner.
