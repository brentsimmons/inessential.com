@title New in NetNewsWire 6: iCloud Syncing
@pubDate 2021-03-17 17:22:50 -0700
@modDate 2021-03-17 17:24:43 -0700
We’ve added — in addition to support for a bunch of online RSS systems — iCloud syncing in NetNewsWire 6. (Latest beta [6.0b3 is recommended](https://nnw.ranchero.com/2021/03/16/netnewswire-b-for.html) at this writing.)

This is great for people who use only NetNewsWire for reading feeds — it means you don’t need an additional service or login aside from iCloud itself, which you’re almost certainly already using.

Here are some things to know…

#### It Reads Feeds Directly

An iCloud sync account is like an On My Mac account in that it reads feeds directly from the sources instead of going through a separate RSS system such as Feedbin or Feedly.

Many people prefer this, for privacy reasons — it means their feeds list isn’t stored on some RSS syncing system.

But some people prefer — also for privacy reasons — *not* to read feeds directly: they like having a system that goes directly to the sources. This way the sources don’t see their requests.

Consider your own preference when choosing to use iCloud sync or not.

Another issue with this model: you could miss articles in fast-moving feeds. (This is true for both iCloud and On My Mac accounts.)

Imagine a feed that updates a hundred times a day. Say you take a Monday off and don’t launch NetNewsWire on any device. By Tuesday, when you launch NetNewsWire, some of the articles from Monday have already fallen off the feed. You’ll never see those articles.

If you used an online system you would not miss those, because online systems never take a day off.

#### It Works with NetNewsWire Only

Other RSS readers include iCloud syncing. But you can’t sync those apps with NetNewsWire via iCloud — Apple’s CloudKit doesn’t allow for that. Each app gets its own storage, and other apps can’t see that storage. (Which makes sense.)

If you want to use NetNewsWire on one machine and another app on another, you’ll need to choose an RSS syncing system that both apps support. (Which shouldn’t be difficult.)

#### NetNewsWire Supports Multiple Accounts

This is not new in NetNewsWire 6, but it’s worth pointing out: you can have an iCloud sync account *and* (for instance) a Feedbin account. NetNewsWire is designed for this, just as Mail is designed for multiple email accounts.

Being able to choose which feeds are synced where is powerful.

But do note that you can have only one iCloud account in NetNewsWire. (Because of how iCloud works.)

#### It May Be Slow at First

NetNewsWire itself is very fast. But syncing happens at the speed of iCloud — and iCloud sometimes throttles the app: it tells NetNewsWire to back off and try again later.

This can be especially noticeable when you’re just starting off with iCloud in NetNewsWire, or whenever you add a big number of feeds, because there will be a ton of data to upload.

So: be patient right at first and whenever you’re adding a bunch of feeds to your iCloud account.

#### We’re Shipping the Mac App Before the iOS App

This feature will come to NetNewsWire for iOS too, of course. Our plan is to ship NetNewsWire 6 for Mac first, and then start TestFlight builds for the iOS app, and then ship NetNewsWire 6 for iOS.

The good news: the iCloud sync code is shared between the two apps, which means it’s already getting a thorough test.

You might ask why we’re not shipping Mac and iOS at the same time. Our wonderful, remarkable team of volunteers — working during their spare time *during a pandemic and multiple other crises* — could have handled shipping both at the same time. But splitting it up this way is my call — it’s easier for me personally to manage, and I ask for your understanding. Thanks!
