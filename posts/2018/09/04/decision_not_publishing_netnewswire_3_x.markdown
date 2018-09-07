@title Decision: Not Publishing NetNewsWire 3.x
@pubDate 2018-09-04 13:26:25 -0700
@modDate 2018-09-04 13:26:25 -0700
The last build of the full version of NetNewsWire, before the sale to Black Pixel, was 3.3.2. I’ve learned that lots of people still use it!

I was considering publishing the source on GitHub and/or making a 3.4 build that strips out the Esellerate and Google Reader syncing parts.

So I sent the code to [Daniel Jalkut](https://indiestack.com/), who quickly hacked at it and got it running and sent it back to me.

And then I ran it too — and quickly realized a few things:

1. It has _lots_ of bugs. Bugs that would be difficult to fix without rearchitecting critical parts.
2. It uses WebView a ton, which is deprecated, and replacing use of WebView with the new WKWebView would not get us the results we want. (The Combined View wouldn’t survive, for one thing.)
3. It would be an attractive nuisance — some people would focus on this while I’d rather the focus be on NetNewsWire 5. I care about history, but not at the expense of the future.

I might still make a build of [NetNewsWire Lite 4.0](https://github.com/brentsimmons/NetNewsWireLite4) available. That code base is not just newer than 3.3.2, it’s just plain way better.

(It was the start of my never-completed NetNewsWire 4 rewrite. NetNewsWire Lite 4, when it shipped, had zero known bugs, and just one known bug within a couple weeks. It was a good app. With modern tools I bet I could find more bugs pretty easily, though.)

But it’s still not nearly as good as the code I’m working on *now*. (Which should be no surprise — it’s years later, and I’m a better developer.)
