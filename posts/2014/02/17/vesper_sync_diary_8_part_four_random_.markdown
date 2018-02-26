@title Vesper Sync Diary #8 part four - Random IDs
@pubDate 2014-02-17 10:34:11 -0800
@modDate 2014-02-17 10:40:53 -0800
After I posted about transforming a UUID into a 64-bit integer I had some interesting feedback from <a href="https://twitter.com/smarx/status/435304040142876672">Steve Marx</a> and <a href="https://twitter.com/marcoarment/status/435453398612443136">Marco Arment</a>: why not just generate a random 64-bit integer?

I don’t think I’ve ever used random numbers in all my years of shipping code. I’ve always figured that if I’m deliberately introducing randomness, then I’m doing something wrong.

So it never would have occurred to me — but in this case it’s perfect.

It also occurred to me that I can check for collisions on generating an ID just by maintaining a set of the existing IDs. (Recall that IDs need to be unique per-account, not system-wide.)

This means a collision could happen only in the set of un-synced notes for a given account, which will tend to be very, very small to zero.
