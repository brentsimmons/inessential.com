@title Blog Engine Choice
@pubDate 2014-10-04 12:01:15 -0700
@modDate 2014-10-04 16:21:52 -0700
Feedback about blog engines was mixed.

<a href="https://wordpress.org/">WordPress</a> was the most frequent suggestion. Other suggestions: <a href="http://fargo.io">Fargo</a>, <a href="http://jekyllrb.com">Jekyll</a>, <a href="http://engineer.readthedocs.org/en/master/">Engineer</a>, <a href="http://v2.getkirby.com/docs">Kirby</a>, <a href="http://www.squarespace.com">Squarespace</a>, <a href="http://middlemanapp.com">Middleman</a>, <a href="http://gohugo.io">Hugo</a>, <a href="https://github.com/cliss/camel">Camel</a>, <a href="https://ghost.org">Ghost</a>, <a href="http://mbutterick.github.io/pollen/doc/">Pollen</a>, <a href="http://buildwithcraft.com">Craft</a>, <a href="http://prose.io/">Prose</a>, <a href="http://blosxom.sourceforge.net">Blosxom</a>, and <a href="http://octopress.org">Octopress</a>.

And <a href="http://blog.svpino.com/2014/10/03/do-you-need-a-new-blog-engine">Santiago Valdarrama suggested</a> I should stick with my current homegrown blog engine.

#### The Requirements, again

I could rule out almost all of these right away.

Many of these suggestions would just replace what I have today — but with *less* functionality. My current system at least works with <a href="http://www.red-sweater.com/marsedit/">MarsEdit</a> running locally, but many of these don’t. MarsEdit (<a href="http://xmlrpc.scripting.com/metaWeblogApi.html">MetaWeblog API</a> support) is not optional.

I wanted something that runs on a server that allows me to post from an iPhone and iPad when I’m away from home. Ideally there would be a native app with a sharing extension, but I could be flexible on that.

WordPress was the obvious best fit. (Works with MarsEdit and has a native app.)

#### The Work Involved

WordPress deserves top billing in a hypothetical web app hall of fame. It’s a remarkable achievement, and I have nothing but respect for the good folks at Automattic.

But I started thinking about importing my blog into WordPress and making sure the content and the URLs all remained the same. I thought about editing a theme to get it to match the current look of the site. And it started to seem like *work*, and not the kind of work that’s much fun (to me).

So I went back to thinking about what I have now. Which is:

* A <a href="http://inessential.com/2009/01/30/new_publishing_system_tour_of_my_head">static blog generation system written in Ruby</a>. It’s fast and bug-free.
* A <a href="https://gist.github.com/brentsimmons/9398899">CGI script that implements the MetaWeblog API</a>, so that the blog generator works with MarsEdit.

What separates this system from the system that I want? Two things: it doesn’t run on a server, and there’s no app or browser-based UI for posting from iOS.

The first one is fairly easily solved: I could put it on a server. The CGI script, perhaps converted to a Sinatra app, would run on some port other than 80, while Nginx serves the static pages that the system generates. I’d also have to deal with Mercurial — the copy of the blog on the server would have to be the parent repository. None of this is difficult, and it feels like less work than moving to WordPress.

That leaves the issue of posting from iOS. I could do a browser-based UI, or — here’s where this starts sounding *fun* — I could write an iOS app just for me.

So that’s what I’ll do: I’ll write an iOS app with an audience of one.

It will give me the chance to work with some technology where I need practice: auto layout and size classes, adaptive UI, storyboards, Core Data, sharing extensions, and Swift.

And then I’ll be able to post from anywhere, any time, which is exactly what I want.

PS I mentioned that my static blog generator is fast. It takes about 10 seconds on my MacBook Air to generate this entire site, which goes back to 1999. (And I have ideas on speeding that up a bit. The generator has some features that I’ve never used, that I could remove and get a performance boost.)

PPS My friend Jake Savin has been writing about moving his Manila blog to WordPress. Here’s <a href="http://www.jakesavin.com/2014/09/11">part one</a> and <a href="http://www.jakesavin.com/2014/10/03">part two</a>. (My blog — this blog, inessential.com — also started out as Manila blog back in 1999. Originally it was just for developing Manila’s static-rendering feature, which I was writing. And then I kept the blog going. Of course, I felt at the time like I was *late* to blogging.)
