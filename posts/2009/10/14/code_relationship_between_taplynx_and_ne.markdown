@title Code relationship between TapLynx and NetNewsWire
@pubDate Wed Oct 14 10:22:22 -0700 2009
@modDate Wed Oct 14 10:23:31 -0700 2009
The code behind TapLynx and NetNewsWire for iPhone are similar — there is plenty of overlap — but they’re not the same.

#### Database engine

TapLynx is the engine I originally wrote for NetNewsWire 2 for iPhone. But then, in a decision that’s easily second-guessable, I wrote a <i>new</i> engine for NetNewsWire for iPhone. The TapLynx version is mature: the one in NetNewsWire for iPhone is much less mature.

TapLynx was originally an iPhone OS 2.x project: it uses SQLite (via FMDB) instead of Core Data. But when I went to write NetNewsWire 2, Core Data was newly-available on the iPhone, and I was convinced that it’s the future.

And it <i>is</i> the future, and I plan to switch TapLynx over to Core Data — but the code needs some more work first.

So, in a nutshell, NetNewsWire for iPhone is the more cutting-edge of the two apps in terms of code. But I’m fixing those cutting-edge bugs: and, once fixed, I believe the Core Data version will be great for TapLynx.

#### The syncing difference

Another big difference between TapLynx and NetNewsWire is how it reads feeds. NetNewsWire syncs with Google Reader; TapLynx reads feeds directly from the source. TapLynx doesn’t have to sync subscriptions or read states or starred items or anything like that.

Syncing and reading feeds directly are very, very different, and will get more so as I make NetNewsWire’s syncing more efficient.

TapLynx has it easy. :)
