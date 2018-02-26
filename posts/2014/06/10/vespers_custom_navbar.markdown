@title Vesper’s Custom Navbar
@pubDate 2014-06-10 13:42:49 -0700
@modDate 2014-06-10 13:43:37 -0700
We don’t use a regular UINavigationBar with Vesper. (We don’t even use a UINavigationController.) What appears to be the navigation bar is a custom view that doesn’t descend from UINavigationBar.

The reason for that is that we have transition animations that I don’t know how to do using a UINavigationBar. Here’s a screenshot of the navbar as you’re swiping back from detail to timeline view.

<img src="http://inessential.com/images/vesper-navbar.png" width="639" height="125" alt="Vesper navbar screenshot" />

Note that the <strong>&lt;</strong> and <strong>+</strong> buttons are at full opacity and don’t move, while All Notes and the icons are in mid-fade. (And All Notes is moving from left to the middle of the navbar.)

The reason for this is that the leftmost and rightmost buttons appear in both timeline and detail view, and in those same locations, so it’s nice that they don’t animate at all.

My question: is there a way to accomplish this using a real UINavigationBar? I like custom UI and our design, but I’m much happier when the implementation can be based on the standard stuff.

I think I made the right call — the only call possible. But I’d love to be wrong.
