@title Hard Syncing
@pubDate 2015-03-04 14:19:14 -0800
@modDate 2015-03-04 14:19:14 -0800
I can’t stand to read App Store reviews (mine or anybody else’s) — but I was told earlier today that [Vesper](http://vesperapp.co/) had a one-star review where the reviewer suggested we use WebDAV syncing.

Sure, we could do that — I thought — if I spent a year on that and did nothing else.

I also work on [OmniFocus](http://www.omnigroup.com/omnifocus/), which has WebDAV syncing, and it lets you use your own server or Omni’s. For free. This is a *great* feature, especially for companies and institutions required to keep all data in-house.

But here’s the thing: syncing is relatively easy if you treat it as a species of web services. That is, if the server side is a smart server with an API and a database, it’s not *that* bad. (Syncing is still hard, but this is the easiest way.) This is how we do it with Vesper.

Syncing by reading and writing files on a generic storage system, on the other hand, is much, much harder. It’s to Omni’s massive credit that they did this.

It’s not just harder to write, it’s also harder to support, since servers will have bugs or be misconfigured. But Omni has the resources to handle this.

This goes back to the discussion of [Sustainable Software](http://mjtsai.com/blog/2015/03/04/sustainable-software/). Features are economic decisions.

Say I looked at it more closely and decided we could do it in six months instead of a year, including at least a month-and-a-half of concentrated beta testing with lots of different servers. We ship in six months (with no other updates during that six months, and definitely no Mac version). We raise the price to $24.99. We hire a support person.

If it were you, would you take that risk?
