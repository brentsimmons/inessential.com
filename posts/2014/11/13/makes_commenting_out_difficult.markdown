@title The Case Against } else {
@pubDate 2014-11-13 15:00:00 -0700
@modDate 2014-11-13 15:00:00 -0700
Sometimes I see code like this:

<code>if {</code><br />
<code>&nbsp;&nbsp;&nbsp;&nbsp;…stuff…</code><br />
<code>} else {</code><br />
<code>&nbsp;&nbsp;&nbsp;&nbsp;…other stuff…</code><br />
<code>}</code>

That’s pretty much a-okay with me.

*Pretty* much. Until I want to comment-out the <code>else</code> block. There’s no way to do a line-wise selection and hit cmd-/ (when it works) and comment out just the <code>else</code> block.

<i>Update 3:15 pm</i>: <a href="https://twitter.com/danmactough/status/533034241899364352">Dan McTough reminds me</a> that there *is* a way to do this. My objection is that it’s more difficult and requires more paying-attention. It’s easier to go to the start of a block and select to the end — it requires almost no thought.

Also: many people like <code>} else {</code> on the ground that it makes it easier to notice the <code>else</code>. Okay.