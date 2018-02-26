@title NetNewsWire and Syncing: Speculation
@pubDate Mon Jul 01 16:14:26 -0700 2013
@modDate Mon Jul 01 16:14:26 -0700 2013
Black Pixel has not elaborated on its plans for sync, other than that [there will be sync](http://blackpixel.com/blog/2013/06/netnewswire-4-open-beta.html). But if we speculate as [Marco did](http://www.marco.org/2013/06/28/all-or-nothing) that Black Pixel is writing its own system (we don’t know this), we might also imagine some reasons why.

#### 10 Years and the Ashes of Other Systems

NetNewsWire Lite 1.0 shipped in late 2002; NetNewsWire 1.0 shipped in early 2003.

Over the span of its life it has synced via Bloglines, NewsGator, .Mac, and Google Reader. None of these syncing systems still exist, but NetNewsWire continues.

Were I in charge of NetNewsWire, this alone would clinch it. I’d write my own system.

The reason is simple: if you can rely on a system to *actually exist*, you can avoid putting your users through the periodic upheavals of switching from one system to another. You can avoid having to rewrite the client side of syncing every few years — and you have more time to spend on making the rest of the app awesome. (I know about this from experience.)

I don’t know if Black Pixel has thought about it this way. (They haven’t said what their syncing plans are.) I like to think that with an app that’s been around this long, they’re looking at the past and taking the long view and laying the best possible foundation for another 10 years of NetNewsWire.

#### Hell Is Other People’s Syncing Systems

Syncing is too critical to the app to leave to someone else’s control. Says me.

While working on Google Reader syncing I ran across some difficult issues. One was that NetNewsWire supported nested folders, and Google Reader didn’t.

This wasn’t the first or only mis-match I’d seen. It’s just a good example that the data model of a given app won’t necessarily match the data model of somebody else’s syncing system. (Another one: Google Reader didn’t allow some characters as part of tag names, while those were legal in folder names in NetNewsWire.)

Other syncing systems tend to have unexpected limitations, too. Google Reader didn’t track read/unread status for articles over a month old or after clicking mark-all-read in a feed when at Google Reader.

And those syncing systems tend to be written by web people. Intelligent, experienced web people — but not necessarily people who have experience creating APIs for mobile apps. Mobile apps need efficiency above everything else. Efficiency is more important than cloning Google Reader’s (undocumented and un-lovely) API and more important than adhering strictly to REST. (Because efficiency makes for a better user experience, and that’s more important than anything else.)

Finally: what if you wanted to sync NetNewsWire’s tabs? Or preferences or smart feeds? Other syncing systems won’t necessarily support these extras — but a NetNewsWire-specific system could support those.

#### The Point

By creating their own system — if that’s actually what they’re doing — they could, theoretically, create a syncing system that’s faster and more efficient than the others and that fits NetNewsWire perfectly. And they’d control it. They’d be able to fix bugs and add features themselves.

The point of all this would have to be user experience. The point would have to be to make NetNewsWire better than other RSS readers.

That’s a lot to do. How well they do it (if that’s what they’re doing) is, as always, the key.

#### But We Don’t Know

They could be writing their own system. They might offer just that, or they might offer that plus one or more other systems. They might open up their system to other RSS readers, and might not. Could be anything. We don’t know, and Black Pixel hasn’t said.

But I’ve got a popcorn maker and a keen interest.
