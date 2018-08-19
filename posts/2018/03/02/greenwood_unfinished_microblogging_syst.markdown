@title Greenwood: Unfinished Microblogging System
@pubDate 2018-03-02 22:06:25 -0800
@modDate 2018-03-02 22:06:25 -0800
A year ago I was working on a microblogging system and wrote a bunch of it, but I didn’t actually finish it.

When I realized it’s not what I actually want, I shelved it.

But interest in microblogging has grown since then — thanks to [Micro.blog](https://micro.blog/) — and so I [posted my code on GitHub](https://github.com/brentsimmons/greenwood) just in case somebody else wants to fork it and do something with it.

The app is called Greenwood. Partly because I like the freshness it evokes — it’s a great name for a fresh, simple start — and partly because Greenwood is the neighborhood next to mine (I’m in Ballard), and I’ve been giving things Pacific Northwest names lately.

<p style="text-align:center">* * *</p>

Blog posts are stored as separate files on disk. There’s a place for attributes at the top of each file, and then the rest is Markdown.

It’s written in Ruby; it’s a Sinatra app. It’s fast. I tested it using eight years of inessential.com’s files.

My plan was to put it in front of a caching Nginx server, so it would essentially run as fast as a statically-rendered site.

There’s surprisingly not much code. And, well, that’s because it’s unfinished.

And — as it says at the top of the README in the repo — DO NOT DEPLOY THIS APP AS-IS. IT IS *NOT* SECURE.
