@title Ian on the Responder Chain
@pubDate 2014-08-20 15:23:56 -0700
@modDate 2014-08-20 22:05:55 -0700
Ian McCullough, <a href="http://ipmcc.bitbucket.org/responder-chain-redux.html">Responder Chain Redux</a>!:

>Guy indicated that he feels like the decoupling offered by the responder chain is too great — that sending an arbitrary message up the chain, with only the sender for context, is insufficient to convey user intent.…

>The delegate-based approach also “cuts off” the chain early, and the argument seems to be that it cuts it off at the “right” level: where context first appears. But what if there’s more than one “right” level, or more than one scope of context?

I’ve always taken it as a clue that action methods take <code>(id)sender</code> as parameter — which I take to mean: “Here’s an action name and a thing. Figure out what to do.”

This is probably more true on Macs, since sender might be a button, menu item, whatever, and the action method may have to do some digging to figure out intent.

But if it’s deterministic and not a guess, is that wrong? I’m not sure.

<i>Update 10:00 pm</i>: <a href="http://kickingbear.com/blog/archives/478">Guy responds on his blog</a>:

>When the table view cell was asked to perform an action it could simply pass it up the responder chain with itself as the sender. With the simple convention of an <code>-(id)representedObject</code> method (or Protocol if you want to be fancy) we can at least glean from the sender which item to act upon.
