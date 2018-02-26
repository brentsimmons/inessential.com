@title Safari Hiding Links Bug
@pubDate Fri Sep 07 18:09:57 -0700 2012
@modDate Sat Sep 08 11:31:13 -0700 2012
I keep noticing a bug where in some cases Safari will not display a link. I’m not sure when it started, but it’s not new with OS X 10.8.1.

I’ve seen it on this site before.

You can see it in action right now on another site — go to <a href="http://andrewsullivan.thedailybeast.com">Andrew Sullivan’s weblog</a>. Find the phrase “Christopher Matthews if the Fed will act:” — there’s a missing word and a missing link.

(That’s not the only example on the page.)

Guess it’s time to figure out a reproducible case and file a bug report.

<i>Update 11:20 am Sep. 8, 2012:</i> I could reproduce the bug on two machines. Neither of those machines use any Safari extensions — but they <i>do</i> use a custom style sheet I created for blocking ads. (At least I <em>think</em> I created it. I’m not positive.)

That style sheet had a line like this:

<code>a[href*="feedburner"],</code>

This prevented links that include the text “feedburner” from displaying. Normally this would be okay, except that so many links that come from news readers include <code>?utm_source=feedburner</code>. So I commented-out that line.

(In case you want to look at my CSS file, it’s <a href="http://ranchero.com/downloads/adBlocking.css">here</a>.)

