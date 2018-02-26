@title Interface Builder Again
@pubDate 2014-12-17 10:56:03 -0800
@modDate 2014-12-17 10:56:03 -0800
This post of mine, almost two years old — [How Much, or How Little, I Use Interface Builder These Days](http://inessential.com/2013/03/06/how_much_or_how_little_i_use_interface) — was referenced on Twitter recently.

It’s worthwhile to revisit these old posts when things change. And my use of Interface Builder has changed quite a bit since writing that post.

Here’s what’s changed:

Auto layout has become more and more a required thing. Recently I was doing layout the old-fashioned way on OS X — using <code>resizeSubviewsWithOldSize:</code> — and, in the specific context where I was using it, it didn’t work correctly. (The layout wasn’t actually updated without resizing the window or similar trickery.) This tells me that to stick with the old-fashioned method is to commit to frustration.

This would be terrible news, but Interface Builder’s auto layout support is much improved since that old post. It no longer creates unasked-for constraints as I’m working. That’s huge.

Some other good things have happened. We have storyboards on Macs now, which make it easier to manage things like preferences windows and login/create-account flows.

And we now have [IB_DESIGNABLE and IBInspectable](http://inessential.com/2014/11/08/first_go_at_using_ib_designable_and_ibin), which makes Interface Builder more useful for designers, which is great if you’re like me and want your designers to have as much direct manipulation as possible.

So. A few good things, taken together, tipped me over, and these days I use Interface Builder a ton.
