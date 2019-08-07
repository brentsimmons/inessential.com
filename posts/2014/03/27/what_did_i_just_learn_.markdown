@title What Did I Just Learn?
@pubDate 2014-03-27 14:37:32 -0700
@modDate 2014-03-27 14:41:48 -0700
I posted about [why I’m not running my own server](/2014/03/27/on_running_your_own_servers_and_why_we) — and then my site went down. (Almost down. Super-slow.)

If it had been my own server I could have rebooted Apache (assuming that was the problem) and had it back up quickly.

Instead I emailed support. It was back up in 15 minutes.

The quick and obvious answer is that this site should be on my own server. But it’s more complicated than that.

This site is hosted on an inexpensive shared-hosting plan on [DreamHost](http://www.dreamhost.com/). It’s been there — along with some other sites and my email — for about 10 years. I’ve been quite happy with the performance and customer support the entire time.

This site is a [statically-rendered site](/2009/01/30/new_publishing_system_tour_of_my_head), and it stands up to [Daring Fireball](http://daringfireball.net/) and [Hacker News](https://news.ycombinator.com/) and everything else without even blinking. (Example: Hacker News linked to that crazy [$1,850 opt-out thing from Network Solutions](http://inessential.com/2014/01/21/network_solutions_auto-enroll_1_850) — and I saw the following [comment on Hacker News](https://news.ycombinator.com/item?id=7099733): “I was really pleased with the instantaneous load of this blog.”)

#### Had This Been My Own Server

Were this blog on my own VM or machine I would have noted the outage and immediately worried if the server had been hacked or was suffering from a DOS attack. If hacked, how would I know?

But — most likely — I would have fixed the problem very quickly by restarting the server software.

Unless I was asleep. Or on an airplane. Or out with friends. Then I might not even have known about the issue.

*That’s* what I like about shared hosting for static sites: other people notice when there are problems, and other people have responsibility for fixing them. Since it’s a static site, if I don’t like the service for any reason I can easily move.

The drawback is that I can’t necessarily fix an issue quickly. It may take 15 minutes. (Or more or less.)

#### What Worries Me

So I’ve established that my site can handle serious traffic. But there’s something I hadn’t thought about before — what about *extremely concentrated* bursts of traffic?

A link from Daring Fireball or Hacker News certainly brings a lot of visitors, and seemingly all-at-once. But there are degrees of all-at-once.

I tweeted my post. That brings a bunch of traffic very quickly, and that’s never been a problem. Then Marco retweeted it — and traffic immediately spiked more than normal for a new post. (Google Analytics real-time view made that clear.)

So my theory is that Twitter links bring in way more concentrated bursts of traffic. Daring Fireball hits are spread out just enough that it has no impact on performance, but Twitter links can swamp a server. (Is my theory.)

#### If That’s True

I don’t know if that’s true — I have to spend more time observing. (If Marco retweets this, and the server gets slow again, then that’ll be a good indication.)

If it *is* true, then I need to find another solution, because I can’t have this blog non-responsive at the exact moment people want to read something here.

#### Possible Solutions

I could pick another shared-hosting provider that can handle crazy traffic bursts. Problem: I don’t know who that would be. They’re all going to claim that they can.

Or I could write a little Node.js blog rendering/caching server and set it to autoscale instances as needed. In theory (in theory) this would work splendidly, but it could get costly. (And it would mean writing some code.)

Or I could could get a VM — say the [$5/month plan from Digital Ocean](https://www.digitalocean.com/pricing/). For a static site I’d just need Apache or Nginx and a hard drive for my files. Sounds simple, and a gentle way to dip my toes into running my own server.

But would that actually be fast enough to handle a Marco-spike? And what happens if — again — I’m asleep, on a plane, or otherwise away from my computer?

The cheapest play, and best for me in terms of learning new things (which is not nothing), is the VM.

But could I sleep?
