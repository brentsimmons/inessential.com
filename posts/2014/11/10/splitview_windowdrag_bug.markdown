@title When Split Views and Windows Fight for Your Mouse
@pubDate 2014-11-10 11:40:00 -0700
@modDate 2014-11-10 11:40:00 -0700
It takes precision mousing to reproduce this, but I bet you can do it.

Launch Contacts.

Note that you can click-and-drag in a bunch of places to move the window. Click in the sidebar or in a profile where there’s no content — you can move the window. Cool.

Now for the precision mousing part: move your mouse to the second split view divider (between the alphabetized list and the profile pane). Move to right below the top of the window. Hover exactly over the divider (note the resize cursor). Then click and drag.

Even though the cursor shows a splitview-resizing cursor, the window moves.

And sometimes the split view divider changes position as the window moves. It’s weird.

I think I know what’s going on:

* <code>movableByWindow&#8203;Background</code> is YES for the window.

* The NSSplitView returns YES for <code>mouseDown&#8203;CanMoveWindow</code>.

It seems to me that if the splitview-resizing cursor is shown, then any click-and-drag should resize the split view and *not* move the window, even when the above two things are true.

I’ll file a Radar.

<i>Update 11:55 am</i>: Bug filed. <a href="rdar://18929475">rdar://18929475</a>