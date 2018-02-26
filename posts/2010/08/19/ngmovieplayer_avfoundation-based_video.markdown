@title NGMoviePlayer - AVFoundation-based video player
@categoryArray Cocoa-Development
@pubDate Thu Aug 19 11:59:50 -0700 2010
@modDate Fri Feb 18 11:55:38 -0800 2011
I put up on bitbucket <a href="http://bitbucket.org/brentsimmons/ngmovieplayer/src">NGMoviePlayer</a> — it uses AVFoundation to play movies. It does some of what MPMoviePlayerControllerView does.

(I had to write a custom movie player because of a bug in iOS 4 where after you play a movie that’s embedded in a UIWebView, MPMoviePlayerController won’t work as expected: it plays just a few frames and then automatically pauses the movie. &lt;<a href="radr://8326264">radr://8326264</a>&gt;)

In writing this code I used a few things that were new to me: AVFoundation, blocks, and UIGestureRecognizer. (I got to do some learnin’, in other words.) (I still have to support older OSes with most of my code, and sometimes it takes a while before I get to use the cool new stuff.)

Side note: one of the interesting things about AVFoundation is that the headers say it will be available for Mac OS X 10.7.

Anyway... if this helps somebody out there at some point, then cool.
