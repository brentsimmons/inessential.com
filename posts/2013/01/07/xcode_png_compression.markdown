@title Xcode PNG Compression
@link http://imageoptim.com/tweetbot.html
@pubDate Mon Jan 07 20:05:28 -0800 2013
@modDate Mon Jan 07 20:52:14 -0800 2013
This <a href="http://imageoptim.com/tweetbot.html">case study by the ImageOptim</a> folks shows that Xcode PNG compression isn’t so great.

>Xcode-optimized images were significantly slower to display. Decoding speed appears to be correlated to image file size more than anything else (most likely savings on byteswapping are negligible compared to additional disk I/O and extra data to decompress).

(This test was done in March 2012, but I only just saw it today. It’s possible I’m the last person to get the news.)
