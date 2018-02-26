@title On Running Your Own Servers, and Why We’re Not
@pubDate 2014-03-27 12:01:26 -0700
@modDate 2014-03-27 12:04:59 -0700
In [Web Hosting for App Developers](http://www.marco.org/2014/03/27/web-hosting-for-app-developers), Marco makes some important points.

One is that high-level cloud hosting (think of Node.js hosts, for instance) may come with “unexpected changes, limitations, and costs.”

Another is that you can save yourself from these problems by running your own servers — and “running your own servers really isn’t hard” and you can set up reliable servers that require a minimum of administration.

I don’t disagree.

It’s entirely possible that Q Branch will run its own servers some day. But we’re not right now, and I’ll explain why.

(Actually, we do have an internal-only server at [MacMiniColo](http://macminicolo.net/). Great service. But we’re not running servers for external services.)

#### Why

I ran servers — as the sole responsible guy (with no got-hit-by-a-bus-policy) — for seven years, from 1995 to 2002.

Many of these were Mac servers — pre-OS-X — which meant they were un-hackable. (Unless you did something remarkably stupid.) But they *could* go down. And did.

Very early in my career I ran one of these in my bedroom behind an ISDN connection. It would crash once or twice a week. I ran a system extension (I forget the name) that automatically rebooted in case of a crash. Sometimes this happened at 4 am and we’d wake up in panic at the sound of the Macintosh startup chime.

One of my Mac servers crashed and never came back — the hard drive was fried. (Code name “Roma.” An old [8500](http://apple-history.com/8500) that I cherished. *Great* computer. I’m still using the Apple Extended Keyboard II that came with that machine.) My second blog was on that machine and it was gone. (This blog is my third blog.)

Later I also ran Windows and Linux boxes (late ’90s, early ’00s). One of the Linux boxes was hacked and apparently used in a DDOS attack. I hadn’t updated BIND quickly enough.

These should have been in a data center, but instead we ran a T1 to my house and called it a data center. Primitive days.

Times have changed, obviously. I’d run VMs in a real data center, and have good backups, and way better admin tools.

But the thing that I *hated*, that I couldn’t stand after seven years, was being on call all the time, day and night, for the servers.

#### But. But.

But I’m still on call for our web services. True.

And I do have to do *some* administration. Our hosted services (two Node.js servers, S3, and a database) don’t come without some housekeeping.

And it’s likely that this will all cost more than running our own VMs. And I might run into things I wish were more flexible (hasn’t happened yet, but I grant that it could).

So it’s a matter of degree: running web stuff means running web stuff, no matter how you do it.

But running our own servers has a cost. A month or so for me to feel comfortable enough with it to trust it and myself. (I know myself: that would take a month. A month where I don’t get much, or any, coding done.) And then probably a year of day and night anxiety.

I’m willing to make this particular trade-off: more productivity and less anxiety for higher costs and *possible* inflexibility and limitations down the road.

I’m willing to make that trade-off precisely because I know I *could* run servers, and I could switch later (though not without some pain) if I choose to. And I can see that happening — if not for Vesper, maybe for a hypothetical other app.

Marco writes:

>Most developers reject the idea outright without even trying because it’s unfamiliar and intimidating. It’s considered an extreme, horrible, unfathomable situation that must be avoided at all costs, usually by people who have never tried it.

That may be true of most developers, though not of me. With me I’d just rather wait and see if at some point in the future I *need* to, for whatever reason. (Cost, flexibility, whatever.)

If I don’t, then great. If I do, then I do, and I’ll apply teeth to ammo. But not till then.
