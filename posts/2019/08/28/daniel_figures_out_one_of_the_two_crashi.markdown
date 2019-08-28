@title Daniel Figures Out One of the Two Crashing Bugs
@pubDate 2019-08-28 13:05:46 -0700
@modDate 2019-08-28 13:17:30 -0700
We have a few reports of a crash where the [add-feed-sheet window doesn’t load](https://github.com/brentsimmons/NetNewsWire/issues/897). There’s a line of code with `window!` — because of course we expect the window to have been loaded — and it crashes right there.

This crash made zero sense to me, but Daniel Jalkut figured out the most likely cause and was able to reproduce it: it’s because the person has moved the app (from one folder to another) after launching it, while it’s running, and the nib-loading machinery can’t find the nib, because it’s moved along with the app.

Tip: if you’re going to move an app, quit it first, then move it, and then re-launch it!

At any rate: our fix for this will be to load that sheet on startup, and then recycle it on each use. This fix will go into NetNewsWire 5.0.1.

This just fixes the bug with this one nib, though. A more systematic fix — maybe just a warning to the user suggesting they quit and re-launch — would be a good idea.

File under “bugs iOS developers never have to worry about.” 🐇

PS We have a [5.0.1 beta milestone](https://github.com/brentsimmons/NetNewsWire/milestone/9) now.
