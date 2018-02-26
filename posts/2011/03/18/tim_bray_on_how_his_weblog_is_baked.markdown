@title Tim Bray on how his weblog is baked
@pubDate Fri Mar 18 14:31:27 -0700 2011
@modDate Fri Mar 18 14:31:27 -0700 2011
Tim explains <a href="http://www.tbray.org/ongoing/When/201x/2011/03/18/Baking-ongoing">how ongoing is baked</a>. Nice solution. I love reading stuff like this.

My own solution is ridiculously heavy compared to his. It rebuilds the entire site (on my hard drive) on every publish. But it has the previously-built version of the site on disk, and writes only the files that have changed. Files that haven’t changed don’t have their timestamp modified.

Then it rsyncs the site to the server. If I’ve changed a template, that might mean every page has changed and so the whole site is sent up. But usually it’s just because I’ve added or edited an article, which means just four or five files get sent.

It’s totally brute-force — but surprisingly fast, even for an 11-year-old site like this one. (If I had a Flash drive I bet it would be even faster.)

I still get to write using <a href="http://www.red-sweater.com/marsedit/">MarsEdit</a>, by the way. It talks to <a href="http://en.wikipedia.org/wiki/WEBrick">WEBrick</a> running on my laptop.
