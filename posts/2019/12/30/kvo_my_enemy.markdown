@title KVO, My Enemy
@pubDate 2019-12-30 16:53:00 -0800
@modDate 2019-12-30 17:09:13 -0800
One of the keys to the stability of the shipping versions of NetNewsWire is that we don’t allow KVO (Key-Value Observing).

KVO is a false convenience — it’s often easier than setting up a delegate or old-fashioned notification. But to use KVO is to just ask for your app to crash.

And not just crash, but crash in hard-to-figure-out ways.

<p style="text-align:center">* * *</p>

So we don’t let KVO into the app — except, well, we’re using `Operation` and `OperationQueue` for Feedly syncing, and the thing about `Operation` is that it uses KVO to signal when it’s finished. There’s no way of getting around that if you want to use `Operation`.

Okay. Fine. It’s worth it, right? It’s just this one small use of KVO. *Surely* we’ll be fine.

[Nope.](https://github.com/brentsimmons/NetNewsWire/issues/1481)

KVO is why I drink.
