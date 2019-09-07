@title On Syncing NetNewsWire Using iCloud
@pubDate 2019-09-06 17:44:21 -0700
@modDate 2019-09-06 17:44:21 -0700
People have been asking me about supporting iCloud as a sync method for NetNewsWire.

It would be really cool because:

* There’s no sign-in
* It’s free — no need to spend money on another service
* It would help broaden the pool of people using RSS, since there would be no additional expense or service they’d need — they could just get going

It’s a great idea — no question. Given that my goal is to get as many people as possible using RSS, this makes total sense.

#### Why we didn’t ship with this feature

For the first release — I still think of it as a 1.0, because it really is — our best bet was to appeal to people already using an existing RSS service. We know that those people like and use RSS, and they’re the people most likely to check out a new RSS app.

(We could have delayed and shipped with support for more existing services, but we figured one was enough to get started with, and we could add other services later. And we are.)

In other words, we tried to make an app that the existing market would like. And that’s the right call when you’re starting out.

Also: iCloud sync makes the most sense when you have both a Mac and an iOS app, and we don’t — the iOS app is still in progress. We totally expect people to use NetNewsWire on the Mac and Unread or Reeder on their iPhone and iPad — and iCloud sync won’t work across apps. This scenario requires using services such as Feedbin.

#### Why I have no idea when this feature might appear

For any existing RSS service, we can be confident that our effort to support it in NetNewsWire would be successful. This is well-trodden ground: we make some web API calls, integrate with our database, and done. It’s not nothing, but conceptually it’s simple and there’s no cause to worry about technical issues.

But iCloud syncing will mean writing exploratory code and only *then* finding out if it’s going to work.

Syncing the feeds list should be relatively easy — the real issue is with syncing read/unread/starred states of articles. That means a *lot* of small records.

Is CloudKit up to this? What are the limits? How fast is it? How reliable?

We just don’t know.

Yes, it’s encouraging that [News Explorer](https://betamagic.nl/products/newsexplorer.html) has this feature — but that doesn't tell us much about the limits, reliability, and performance.

Working on this is a risk.

So — as you can imagine — we’re still more keen on supporting existing RSS services, because we know there are plenty of people who for-sure like RSS, and who might like NetNewsWire, but who won’t switch their syncing system just to use NetNewsWire.

That said: I do think we’ll get around to trying this, and I’ll be super-pleased if it works, because it really is a great idea — but we have a bunch of other work to do first. (Including the iOS app!)
