@title OPML File Type on Macs
@pubDate 2017-01-05 13:20:33 -0800
@modDate 2017-01-05 13:25:40 -0800
I was fixing a bug in <a href="https://www.omnigroup.com/omnioutliner">OmniOutliner</a> where it wouldn’t open a file with an uppercase .OPML suffix. I did some digging, and the fix was to register the app as handling the com.apple.news.opml file type.

Which upset me. I’ll explain.

<a href="http://dev.opml.org">OPML</a> — Outline Processor Markup Language — was invented in 2000 by Dave Winer at UserLand Software. It’s not Apple’s format, and the correct file type is org.opml.opml.

I was working for Dave at the time. Some time after Dave wrote the first OPML reading and writing code, I ported it to C. Later, when I was working on <a href="http://web.archive.org/web/20030201105606/http://ranchero.com/netnewswire/">NetNewsWire</a>, in 2002, I wrote what may have been the first Objective-C code for reading and writing OPML. And today I work on OmniOutliner, which supports OPML, and I’ve published an <a href="https://github.com/brentsimmons/RSXML/blob/master/RSXML/RSOPMLParser.h">open source OPML parser</a>.

So I know OPML. After Dave, I may have worked with this format more than anyone else in the world.

This file type redefinition not only created a bug that I had to figure out and fix, it also demonstrated disrespect. I suspect it was entirely thoughtless — but, well, that’s still bad.

Radar forthcoming.

<i>Update:</i> Bug filed: <a href="rdar://29888756">rdar://29888756</a>.
