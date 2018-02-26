@title What Happened at NewsGator
@pubDate 2014-05-10 16:39:20 -0700
@modDate 2014-05-10 21:48:38 -0700
I sat in the back of the bus the whole time and I don’t really know all the details. But here are the parts that I know about.

NewsGator began by calling itself “The RSS Company.” It was founded by Greg Reinacker, who’d written an [Outlook plugin that was an RSS reader](http://web.archive.org/web/20030225030955/http://www.newsgator.com/) called NewsGator. (NEWS aggreGATOR, right?)

The company got funding, and it then created a browser-based RSS reader and a syncing system. It acquired [FeedDemon](http://www.feeddemon.com/) in early 2005, which gave it two Windows readers and a browser-based reader. The one obvious hole in the line-up — remember that this was before mobile was huge — was a Mac reader. In late 2005 it acquired [NetNewsWire](http://netnewswireapp.com/) and hired me.

NetNewsWire users needed syncing, and many of them used Windows at work, and so they wanted cross-platform syncing. It was a good fit.

So I went to work. A little while in I realized I didn’t have time to do both NetNewsWire and [MarsEdit](http://www.red-sweater.com/marsedit/) well, so we sold MarsEdit to Daniel Jalkut.

#### NGES

But if you have a funded company, you probably need to convince your board that there is the potential for more than just selling software at $25 per copy. You need enterprise money.

Enter NewsGator Enterprise Server. I spent a grand total of perhaps 30 minutes looking at it during my time at NewsGator, so I’m no expert. But the idea was to put NewsGator’s RSS platform behind the firewall.

In addition to straight RSS reading it had some kind of controls for making groups of people. An admin could say, for instance, that all developers are subscribed to these ten feeds, plus whatever else they might want.

I think (memory is hazy, and I really didn’t care) that there was also commenting and rating articles. Sharing too. Intranet-y workflow-y things.

At one point I added a feature to NetNewsWire so that you could put a config file in the right place and it would talk to NGES rather than the consumer system. I’m not sure anyone actually used this feature ever, since Macs weren’t big in the kind of places that installed NGES. (Luckily it was a small feature to add — mainly it just said what the endpoint was.)

[Nick Bradbury](http://nickbradbury.com/), on the other hand, wasn’t as lucky — FeedDemon was popular among NGES users, so he had to do a bit more work.

#### Enter Sharepoint

I don’t know when or how this happened, but at some point NewsGator noticed that the commenting and sharing and social bits of NGES were more interesting than RSS reading itself. It created Social Sites, which was a Sharepoint plugin that provided all that social stuff behind the firewall.

As far I could tell — again, from the back of the bus, where I was working on NetNewsWire — Social Sites was <em>very</em> successful. I don’t recall, and probably couldn’t share, some of the details, except that the company did things like buy everybody a Kindle for Christmas because sales had been so good.

#### But what about RSS?

Somewhere along the way the decision was made to shut down the consumer browser-based app and the syncing platform. (2009? I think.) NetNewsWire and FeedDemon would sync with Google Reader, since that was what customers kept asking for anyway, and it was just about the only game in town.

Fine. NewsGator wasn’t getting out of the RSS business entirely, but its future investment was limited to just the cost of a few people. (Me and Nick Bradbury, essentially.)

The original Outlook plugin, which had been renamed Inbox, was shut down then. (I think. It didn’t make the transition to Google Reader.)

#### Nick B Departs

The iPhone came out, we switched to Google Reader, and, not long after, Nick Bradbury departed. I was still there — and NewsGator had treated me very well all along, and I loved working on NetNewsWire.

While the enterprise side of the company thrived, the consumer side dwindled. We came up with an idea to make a library for making other apps: [TapLynx](http://taplynx.com/). The idea was to use what we knew about iPhone and RSS so that other people could create publications-as-apps without having to do any programming.

We worked with some launch partners: Variety and AllThingsDigital. We shipped some apps. (Those apps are not still TapLynx-based.) People purchased TapLynx licenses and created their own apps. Eventually we realized it needed more resources than we could give it — and better marketing — and we sold it to [Push IO](http://push.io/). (Joe Pezzillo’s and Dan Burcaw’s company.)

#### One Last Shot

It became clear around 2010 or 2011 that NewsGator wasn’t interested in paying me just to work on NetNewsWire. They had come a long way from “The RSS Company” — which is totally fine. They made a successful product which wasn’t an RSS app, and that’s okay. (Nothing gold can stay.)

In fact, I say *good for them*. The software business is difficult, and if the pivot works, you don’t stop just because the original idea for the company was different.

It also became clear to me that I was going to leave NewsGator. The problem, though, was that NetNewsWire was still there.

Walker Fenton and I talked about doing a spin-off — with the encouragement of NewsGator. It included three other NewsGator employees (Brian Reischl, Jenny Blumberg, and Nick Harris) who we thought would be great members of the team.

We called it Sepia Labs. (I like those old-time-y names.) We came up with a product idea: [Glassboard](http://glassboard.com/).

As we were getting started I was working on NetNewsWire 4. I shipped NetNewsWire Lite 4.0 on the Mac App Store, and a couple months later NewsGator sold NetNewsWire to [Black Pixel](http://blackpixel.com/), when I realized I couldn’t give Glassboard the energy it needed if my time was split.

That was a super-hard decision, since NetNewsWire was my baby. But after nine years it was time to turn it over to a bigger team with in-house designers and more programmers.

(I was extremely proud of that last release. It felt great to do one last good thing.)

So it was full speed ahead on Glassboard. Almost.

#### Nick B Returns

We needed an Android developer. My first priority once Walker and I decided to do Sepia Labs was to bring back Nick Bradbury.

I loved working with Nick in the past, and — even though Nick was an iPhone user and Delphi programmer — I wanted him as our Android developer. Nick was not eager to be on the NewsGator payroll again, but he accepted since we were spinning out into a separate company. And he quickly turned into a great Android developer, as we all knew he would.

#### But Glassboard didn’t make much money

The trick with something like Glassboard is that it has to be free because it’s worthless without people using it. But you still want to charge for *something*. We weren’t the first people in that pickle, and there’ll be plenty more people in that pickle.

It *is* solvable, but the solution is unique to each app.

We made some progress, but we didn’t solve it.

#### Surprise!

Though Sepia Labs existed as a company, we didn’t actually complete the spin-off.

Then one day in the summer of 2012 the CEO resigned. (He was the only CEO the company had known.) The new CEO really liked the work we’d done on Glassboard, though he didn’t think the app itself was likely to be financially successful.

So we had a choice:

* Complete the spin-off. Take with us six month’s of funding. Sink or swim.

* Or redo their Social Sites mobile apps for iOS and Android. Make them at least as good as Glassboard.

There was no way that six months would have been enough to become profitable with Glassboard. (Remember that there were six people. Lots of payroll.)

In all my years at NewsGator I’d avoided enterprise work. But suddenly I found myself as a *designer* of Social Sites for iOS and Android. (Nick B did wireframes and the Android app. I did Photoshop mockups and assets. Nick Harris wrote the iOS app.)

I decided to leave. At first I thought I could manage to do some side work instead, but that thought quickly passed in favor of leaving altogether.

I stayed long enough to finish what I’d committed to — I delivered a design for Social Sites for iOS and Android. And then I went straight to work — February 1, 2013 — at Q Branch, where I plan to be for the rest of my career.

#### Coda

After I left, Nick Harris left. Then Walker Fenton, Brian Reischl, and Nick Bradbury left. Jenny Blumberg remains at NewsGator.

But it’s no longer NewsGator. That name didn’t match what the company does, and it was always a little silly. (I remember trying to convince people to change it back in 2005 or 2006.)

(To make things worse, years ago there was some company named Gator that had something to do with spam. Completely different thing, but people got confused sometimes.)

NewsGator acquired Sitrion and changed the name of the company to [Sitrion](http://www.sitrion.com/). (I still call it NewsGator, because I’m talking about the history of the company, not the present day.)

And: NewsGator sold Glassboard to [Justin Williams](http://carpeaqua.com/).

And that’s the tech industry for ya. Everything I brought to NewsGator is now somewhere else. Everything I created while I was there is now somewhere else. Nothing of me remains there — and all I have from the company is a red stapler they gave me when I reached five years of service. (And some money.)

And even NewsGator isn’t NewsGator anymore.

But even though this is a weird long story about change and loss, I have nothing but good feelings for the people there. They’re smart people who made tough decisions — and they treated me exceptionally well. I wish them continued success.

Last things to note: even Google Reader is gone. And AllThingsDigital.

Meanwhile, [RSS is alive and well](http://inessential.com/2013/03/14/why_i_love_rss_and_you_do_too) (from 2013), as always.
