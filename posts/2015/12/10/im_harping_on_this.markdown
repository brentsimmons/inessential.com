@title I’m Harping on This
@pubDate 2015-12-10 15:50:47 -0800
@modDate 2015-12-10 15:50:47 -0800
Look at the Finder for a second. Look at Mail. Open your Safari bookmarks. Look at Xcode’s sidebar.

In each case you have a tree view of *different things*. Under the hood, that view is backed by a data structure which contains *different things*.

Now, those different things have some things in common — an icon and name, for instance. But they’re otherwise quite different.

<p style="text-align:center">* * *</p>

In the bad old days you’d make some kind of subclass for all of these things. Call it ListMember. Your Folder and File class (or whatever) would descend from ListMember.

But these days we’re smarter: we use protocols. There’s no reason Folder and File should descend from the same class — they’re almost entirely different, and inheritance is a pain to deal with, so we use protocols instead.

And we’re happy. It works great.

Until you realize that, in Swift, you <a href="http://inessential.com/2015/07/19/secret_projects_diary_2_swift_2_0_prot">can’t</a> do <a href="http://inessential.com/2015/08/05/swift_diary_9_where_im_stuck">this</a>.

This comes up all the time in my code. I want to love Swift — and <em>do</em>, in many ways — but every time this comes up I want to go back to Objective-C.

Is it just me that has this issue? It seems like it’s a massively common problem. Is everyone but me doing things the old-fashioned way (via inheritance) and just not talking about it?
