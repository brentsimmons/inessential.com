@title Overflow
@pubDate 2014-12-04 09:41:02 -0800
@modDate 2014-12-04 09:41:02 -0800
Ars Technica reports on an <a href="http://arstechnica.com/business/2014/12/gangnam-style-overflows-int_max-forces-youtube-to-go-64-bit/">integer overflow at YouTube</a>.

We had a similar problem with NewsGator RSS syncing years ago — the unique ID for articles went past 2,147,483,647, and some of our client apps weren’t prepared for it. (The server was fine.)

NetNewsWire was okay, because I was paranoid and treated all the IDs as strings. But that was actually too much paranoia — I really should have saved the space and used integers. But if I had, it’s likely I would have had the same problem. I’m not sure I would have thought to use 64-bit integers.

Now, of course, in any similar circumstance, I use 64-bit integers. (Or at least <a href="http://inessential.com/2014/04/13/vesper_sync_diary_13_unlucky_13">53-bit integers</a>.) Lesson learned.
