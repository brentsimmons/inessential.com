@title Where I am with NetNewsWire
@pubDate Sat Jun 06 19:36:25 -0700 2009
@modDate Sat Jun 06 19:40:28 -0700 2009
<a href="http://www.flickr.com/photos/78891836@N00/2167620490" title="View 'Afternoon coffee' on Flickr.com"><img src="http://farm3.static.flickr.com/2288/2167620490_83707e2ba5_m.jpg" alt="Afternoon coffee" border="0" width="180" height="240" hspace="5" align="right" /></a>People ask me what’s up with NetNewsWire — and this week they’ll ask me in person. So I figured I’d better write a post about it.

Here’s the scoop: both versions are in extremely active development. I’m currently working on NetNewsWire 3.2 and 4.0 for Mac and NetNewsWire 2.0 for iPhone.

I recently set up Twitter accounts for them: <a href="http://twitter.com/nnw_Mac">NetNewsWire/Mac</a> and <a href="http://twitter.com/nnw_iPhone">NetNewsWire/iPhone</a>. I haven’t posted much yet, but I will. (You can also follow my <a href="http://twitter.com/brentsimmons">personal account</a>, but I often post things that have nothing to do with NetNewsWire. And I can’t do support via Twitter via any of the accounts.)

I <em>don’t</em> have time estimates — any guesses would be completely wrong. But nobody’s more impatient than I am.

#### What’s coming

You may have seen the <a href="http://nick.typepad.com/blog/2009/04/ann-feeddemon-30-beta-4-with-google-reader-synchronization.html">FeedDemon beta with Google Reader syncing</a>.

The plan is to add Google Reader syncing to NetNewsWire 3.2/Mac and NetNewsWire 2.0/iPhone also. I can’t promise for sure for-sure, but I’m 95% sure.

#### More about NetNewsWire 3.2/Mac

This version, as the number suggests, isn’t a huge upgrade — the main thing is Google Reader syncing. (Plus a couple small features and some bug fixes.) It will be a transitional release — it drops a bunch of stuff, gets leaner, and moves some of the data storage over to the format 4.0 will use.

Here’s what it drops: Tiger support is gone — it will require 10.5 or greater. The DotMac/FTP syncing and Bloglines syncing are gone. Some little features like the Send Email to Author command are gone.

My favorite part is under-the-hood — dropping code I don’t need for Tiger support, mostly. Switching to ObjC 2.0 properties, especially.

#### More about NetNewsWire 4.0/Mac

Work on 4.0 is in parallel with other work — but it’s farther behind. It will also be a bigger upgrade.

I’d talk about what’s going to be in it, but it’s too soon.

Well, I can talk some technical stuff: I plan to move storage completely over to Core Data and I’d like to turn on garbage collection.

#### More about NetNewsWire 2.0/iPhone

It’s a race — I don’t know which will ship first, NetNewsWire 2.0/iPhone or NetNewsWire 3.2/Mac.

I’ve spent the last six months or so mostly in iPhone-land, working on the foundation for NetNewsWire 2.0. Along the way we discovered it was generalizable and that there’s a business doing private-label apps based on the same foundation that will power NetNewsWire 2.0. The highest-profile example is <a href="http://itunes.apple.com/WebObjects/MZStore.woa/wa/viewSoftware?id=316429710&mt=8&s=143441">All Things Digital</a> — if you use it, you are in a way using an early version of NetNewsWire 2.0.

It turns out that learning how to do good news readers on iPhone is harder than I expected. Almost the entire ballgame is about performance.

Think of all that a Twitter client has to do — then imagine running 100 Twitter clients at once. I think I’ve spent about 3 man-months just in Shark and Instruments, figuring out how to scale and perform well on the iPhone, which is for real a new platform, even though we still get to write in Cocoa.

<a href="http://www.flickr.com/photos/78891836@N00/2289878373" title="View 'Destroying the hard drive' on Flickr.com"><img src="http://farm3.static.flickr.com/2221/2289878373_9d0a2a1e2c_m.jpg" alt="Destroying the hard drive" border="0" width="180" height="240" hspace="5" align="right" /></a>(Another thing I spent a lot of time on was UI. NetNewsWire 1.0 for iPhone is quite spartan, you’ve noticed.)

Anyway, the plan is to add Google Reader syncing for NetNewsWire 2.0 — and a few other things, which I don’t have time to write about now.

But it’s all new — taken apart, scrapped, put back together, taken apart again, written anew, etc.

#### WWDC

So, if you see me at WWDC, tell me how <em>your</em> stuff is going. I’m interested. And now you already know how it’s going with NetNewsWire. :)
