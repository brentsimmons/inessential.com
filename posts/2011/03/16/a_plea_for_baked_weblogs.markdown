@title A plea for baked weblogs
@pubDate Wed Mar 16 21:49:49 -0700 2011
@modDate Wed Mar 16 21:51:23 -0700 2011
You’ve noticed that processors aren’t getting faster as quickly as they used to. Instead, manufacturers are adding more cores. This means that app developers, in order to make their software faster and able to handle a bigger load, have been learning new techniques — they’ve been learning to take advantage of multiple cores. (They’ve been learning how to write multi-threaded apps.)

I think there’s a somewhat similar situation in the web-in-general. Servers aren’t getting faster, but traffic’s going up.

And so, even in the year 2011, if your weblog gets <a href="http://blog.23x.net/216/anatomy-of-a-fireballing.html">Fireballed</a>, there’s a good chance it won’t be able to handle it. That seems crazy. It’s not 1997 — it’s <em>2011</em>.

It freaks me out that this is still an issue. Or, worse — sometimes it pisses me off a little, when I want to read something and I can’t. (Imagine when it’s a post on your product’s weblog. I might never come back, or I might get a bad impression of your thing just because your site couldn’t handle a spike in traffic.)

Given that we can’t rely on servers getting faster, but we *can* rely on more and more traffic, weblog developers could learn new techniques to make their sites faster.

#### New technique is old

I think the new technique web developers — or weblog developers, at least — ought to learn is static rendering: writing files to disk rather than building from a database on every request.

It’s an old technique, actually, but too rarely practiced. (Lots of weblogs in the ’90s were rendered as files-on-disk. They were built from a database plus templates and scripts and uploaded to a server. We did a bunch of this when I worked with <a href="http://scripting.com/">Dave Winer</a> at UserLand Software.)

In 2002 Aaron Swartz wrote <a href="http://www.aaronsw.com/weblog/000404">Bake, Don’t Fry</a>, which is worth re-reading. (He also wrote that he doesn’t care about performance. If getting fireballed were a thing back in 2002, he might have cared about performance. If he had seen system X go down for a day, he might have cared about performance. It’s interesting that performance — or robustness — arguably wasn’t an issue in 2002, but it is now.)

#### Two main ways to do this

1. Desktop/laptop to web: in this scenario, your personal machine holds the source. An app or set of scripts generates the website based on templates, then uploads it to the server. (<a href="http://inessential.com/2009/01/30/new_publishing_system_tour_of_my_head">That’s what I do</a> with this site.) It works great: I’m a huge fan of this style of publishing.

2. Dynamic authoring, static publishing: in this scenario, everything lives on the server. You have the advantage of being able to publish from anywhere you can get to a web browser. But then the server generates static pages when you make a change. It’s much like the first scenario, except that it’s accessible from everywhere. (It supports multiple authors better too, for people who need that. Which I myself do, for some sites.)

#### I’m aware of a few things

- Dave Winer is working on new software which I think implements the first scenario. (I <em>think</em>, that is: I need to investigate. I could be mis-characterizing the software.)

- <a href="http://wordpress.org/">WordPress</a> has <a href="http://wordpress.org/extend/plugins/wp-super-cache/">WP Super Cache</a>, which should make your site Fireball-retardant. I use it on a couple sites. But this feels like a temporary band-aid. I keep wondering if we’ll need a WP Super Amazing Cache at some point.

- <a href="http://www.movabletype.org/opensource/">Movable Type</a> can work like the second scenario, but I can’t help but feel that Movable Type is a much-heavier solution than the average blogger requires or wants. It feels like a pro thing, where the average blogger would like something closer to the Twitter end of the blogging spectrum.

- <a href="http://www.blogger.com/">Blogger</a> probably does static rendering. Maybe <a href="http://typepad.com/">TypePad</a> does too. But, to be clear, I’m talking about slightly-geekier-bloggers, the type who install a blogging system on their own server or on their shared space at DreamHost or wherever. Those are the weblogs I tend to read.

#### What I’d like to see

Given the above, I think the still-missing piece is the scenario #2 weblog system. It should be as easy-to-install and easy-to-use as WordPress — easier, actually, would be better. Not-requiring a database at all would be awesome. To be successful, like WordPress it would probably have to be done in PHP, since PHP remains the commonly-installed scripting system on shared webservers.

Maybe such a thing exists already? It’s entirely possible. (Then the next step is marketing it so that people like me hear about it.)

Anyway, I bring this up because I’m tired of slow sites or sites that go dark the <em>very minute I hear about them</em>. It looks to me as if there’s a big missing piece in the ecosystem, and now might be a great time to build that piece. Because, otherwise, it’s not going to get any better.
