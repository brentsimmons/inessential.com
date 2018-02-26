@title Evergreen Diary #4: Send to Micro.blog
@pubDate 2018-01-15 09:35:13 -0800
@modDate 2018-01-15 10:11:09 -0800
The [latest build of Evergreen](https://ranchero.com/evergreen/) adds Micro.blog to the Share menu in the toolbar, if you have the [Micro.blog Mac app](http://help.micro.blog/2017/mac-version/).

It sends the title and link of whatever you’re reading over to the Micro.blog Mac app, and you can edit it before actually posting.

This is *hugely* important. RSS readers exist not to just make reading easy but to make the web a conversation.

The next release will (probably) include [MarsEdit](https://red-sweater.com/marsedit/), for the exact same reason. If you have ideas for other apps to include, let me know (see the bottom of the [Evergreen site](https://ranchero.com/evergreen/) for contact info).

Ideally, every app like Micro.blog and MarsEdit would have a sharing extension — but, where they don’t, I can add them as long as they support some kind of way to do so.

<h4>Technical Details</h4>

Micro.blog supports a URL scheme for sending it a post: see See [SendToMicroBlogCommand.&#8203;sendObject](https://github.com/brentsimmons/Evergreen/blob/151e7140ec8fe6440587c1418806c1ceea256a94/Commands/SendToMicroBlogCommand.swift#L50) for the implementation in Evergreen. (And of course feel free to use any Evergreen code in your app.)

<h4>History</h4>

It’s not that we realized just today that *posting* from an RSS reader is important. Since posting was always an absolute requirement, way back in 2003 I released NetNewsWire 1.0 with an integrated blog editor.

I got that idea from Radio UserLand, which was an RSS reader and blog editor by the company where I worked before I wrote NetNewsWire. It’s [Dave](http://scripting.com/)’s idea, not mine.

By the time I was working on NetNewsWire 2.0, it became apparent that smooshing a blog editor into a reader app meant that the blog editor suffers. The blog editor in NetNewsWire 1.x was pretty darn bad. So I had the idea of splitting out the blog editor to a separate app — inducing mitosis — which you can read about in my [MarsEdit report](http://inessential.com/2004/12/12/marsedit_report) of late 2004.

Mitosis was a success.

One of the keys of that success was that the API for contacting MarsEdit had to be open, and NetNewsWire had to support any blog editor, or any other app, that supported that API — because otherwise I would have been unfairly leveraging success with NetNewsWire on behalf of my new blog editor, and that would have been wrong.

MarsEdit still supports that [interface](http://ranchero.com/netnewswire/developers/externalinterface), and my next step is to write the client side in Evergreen, so it can send to MarsEdit and any other app that supports that interface.

I am, by the way, delighted to be writing code for a 14-year-old API that still works.
