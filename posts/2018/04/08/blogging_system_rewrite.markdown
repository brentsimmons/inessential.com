@title Blogging System Rewrite
@pubDate 2018-04-08 11:37:20 -0700
@modDate 2018-04-08 11:38:15 -0700
I realized that I want my blog to be me on the web. This *used* to be true, but then along came Twitter, and then my presence got split up between two places.

To make this work, I needed two things that my [old system from 2009](http://inessential.com/2009/01/30/new_publishing_system_tour_of_my_head) didn’t provide:

1. Title-less posts, and
2. The ability to run the site generator on my server, not just on my Mac.

In other words, I needed to be able to write tweet-like posts with no title — while on the go, on my iPhone or iPad.

I’ve done #1 and part of #2 — now it’s just a matter of figuring out how to deploy the system to my server (which is a shared host on Dreamhost, but where I can run CGI scripts).

The [code’s up on GitHub](https://github.com/brentsimmons/wildcat). I don’t really expect other people to use it, but you can, if you want to. I apologize in advance for not having time to write extensive documentation or provide support.

The system’s pretty fast: it rebuilds this almost 20-year-old blog in about three seconds on a five-year-old iMac. The code is, I hope, understandable and hackable, and I welcome you to fork it if it interests you.

<p style="text-align:center">* * *</p>

Another part of this: I’ll stop using [micro.inessential.com](https://micro.inessential.com/). This blog will be my blog and my microblog. I want just *one* place that’s me.

I don’t know if I’ll have my posts here automatically echoed to my Twitter account. Maybe. They do already appear on [Micro.blog](http://micro.blog/brentsimmons).

PS Titles were always optional for RSS, but most feed readers don’t handle this well. [Evergreen](http://ranchero.com/evergreen/) was written with this in mind. (It’s not 1.0 yet, though. Working on it!)
