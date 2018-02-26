@title Put weblogs on bitbucket
@pubDate Fri Jun 18 11:36:42 -0700 2010
@modDate Fri Jun 18 11:50:04 -0700 2010
I’ve moved the repositories for inessential.com and ranchero.com to bitbucket and made them public read-only.

<a href="http://bitbucket.org/brentsimmons/ranchero.com/overview">ranchero.com repository</a><br />
<a href="http://bitbucket.org/brentsimmons/inessential.com/overview">inessential.com repository</a>

It’s just the raw stuff that gets rendered into weblog posts — it’s not the rendering scripts. There’s no actual software. Just a bunch of words.

Not sure why I did this. Maybe just because I could. But sometimes big bunches of text can be useful for somebody somewhere.

The actual posts are in the posts directory. Older posts are HTML, newer posts are written in <a href="http://daringfireball.net/projects/markdown/">Markdown</a>. The lines at the top of each post that start with a @ character are metadata. Stuff between &#91;[ and ]] are macros. Stuff between &#91;[= and ]] are includes (grabbed from Snippets folder).

I wrote about my system in early 2009 <a href="http://inessential.com/2009/01/30/new_publishing_system_tour_of_my_head">here</a>. I’ve been quite happy with it. To restate the advantages:

1. Static HTML pages are <em>fast</em>. I don’t have to worry about getting Fireballed. :) And they’re easily portable, if I ever have to change web hosts.

2. Static RSS feeds are fast too, which is good because they get requested a lot.

2. Having source control is especially nice when I’m working on templates.

3. Having source control is great for offsite backups. (I was using Dropbox before I switched to bitbucket. I’ll probably still keep a backup on Dropbox, just because.)

4. Being able to search through my weblogs on my desktop using Spotlight or <a href="http://betterthangrep.com/">ack</a> is very convenient. (Okay, I admit I use ack mostly.)

5. The system can generate a local preview version, so I can render my site just on my machine and look at it before uploading. I don’t use that often, but it’s nice when working on templates.

Best part: I still get to use <a href="http://www.red-sweater.com/marsedit/">MarsEdit</a> — I have a small Ruby-based server that implements the API that MarsEdit expects. I hardly ever actually look at the weblogs as files-on-disk, and I never edit the posts that way (though I could).
