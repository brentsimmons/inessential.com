@title UITextView - The Solution
@pubDate 2014-01-07 21:17:30 -0800
@modDate 2014-01-07 21:51:57 -0800
Before [posting](http://inessential.com/2014/01/07/uitextview_scroll-to-typing_bug) I’d been all over Apple’s developer forums and Stack Overflow, and I’d emailed with people who had appeared to solve my UITextView problem in their apps.

Nothing worked — or, rather, a bunch of things worked somewhat, but they didn’t solve my problem entirely.

So I went through all the help I got on Twitter and tried different things. The *only* things that worked reliably were the solutions that involved adding a delay before scrolling.

The delay appears to allow UITextView to catch up to reality, to complete pending calculations.

You can [download my solution](http://ranchero.com/downloads/TVJumpBug-Solution.zip). (Super-small project.)

#### This Is a Hack

Nobody (I hope) feels comfortable working around a bug this way. Almost every time you’re performing code after a delay you *know* something’s going wrong, and you’re just guessing and hoping that it works.

But here’s the thing: something *has* gone wrong and I *am* just guessing and hoping it works.

Given that it’s a hack, I wanted to use the least amount of code possible.

I ended up adapting [Tanmay’s solution](https://twitter.com/tanmays/status/420656988251377664). (I haven’t downloaded his app [Write](http://writeapp.net/) yet, but it looks pretty cool based on the website. Thanks, Tanmay.)

#### How it works

In `shouldChangeTextInRange` it checks to see if the text is equal to `@"\n"` or `@""`. If it is, it calls `scrollToShowSelection` after a delay of `0.1`.

And then `scrollToShowSelection` checks to see if the selection is at the end of the text. If it is, it sets the `contentOffset` (animated).

That’s it. Pretty simple. And it’s a minimal amount of code, which means it will be easy to rip out once the bug is fixed in iOS. (Or, rather, I’ll leave the code in but have it run only on older versions of iOS. And rip it out eventually.)

#### It Really Is a Hack

So this is an opportunity to talk about when to use hacks like this. The short answer is never. I *hate* doing things like this and I can go years in between.

But the important thing is the quality of the user experience. Nothing else matters.

It’s up to me to do this in the smartest way possible — and to test to make sure it’s solid, and to pay attention to iOS updates to make sure it still works, and to make the code *not run* at the earliest date possible, once the bug is fixed.

Until that day, sleep will be a little more toss-and-turn-ier than normal. (Obligatory: this is why Daddy drinks.)

PS If I saw this in your code, I’d tell you that you’re screwing up. It’s quite okay if you say that to me.

PPS [Doug reminds me to cancel previous performs](https://twitter.com/MouthyFool/status/420794483668549632). He’s right.
