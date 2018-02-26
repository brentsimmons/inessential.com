@title Evergreen Diary #2: Random Notes
@pubDate 2017-12-09 12:57:58 -0800
@modDate 2017-12-09 13:24:33 -0800
I’ve been working on <a href="https://ranchero.com/evergreen/">Evergreen</a> for about three years, and so I considered writing about playing such a long game — but then Daniel released <a href="https://red-sweater.com/marsedit/">MarsEdit 4.0</a> after *seven* years.

I tip my fedora to the master.

<p style="text-align:center">* * *</p>

But there is at least one difference: it’s taking so many years just to get to one-point-oh. I’ve never been on any kind of project that took so long just to get to the initial release.

The app’s been built from the bottom up. Since I knew in advance what I needed, I could write code that wouldn’t get actually used for years.

Here’s a small example, written almost two years ago: [RSHTMLMetadata.h](https://github.com/brentsimmons/Evergreen/blob/master/Frameworks/RSParser/HTML/RSHTMLMetadata.h).

The scoop: it always bugged me that in NetNewsWire, when it was mine, the favicon downloading system never checked the metadata in a feed’s home page to find the favicon.

It always just appended `/favicon.ico` — which wasn’t always correct. So it would get the wrong one or just not find it.

(Note: it’s entirely likely that the <a href="http://netnewswireapp.com/">current version of NetNewsWire</a> has fixed this bug.)

So, a year-and-a-half ago, I wrote code in `RSHTMLMetadata` that pulls the favicon URL from web page data.

And then, just last month, when I finally got around to writing the favicon downloading system, it took very little code to actually pull the favicon URL from a web page (in [FaviconURLFinder.swift](https://github.com/brentsimmons/Evergreen/blob/master/Evergreen/Favicons/FaviconURLFinder.swift)):

<code>let htmlMetadata = RSHTMLMetadataParser.&#8203;htmlMetadata&#8203;(with: parserData)</code><br />
<code>return htmlMetadata.&#8203;faviconLink</code>

This pattern — ground-up development, where you know what you need in advance — isn’t really different from apps developed much more quickly.

The difference is the amount of satisfaction I feel when I finally connect old and new pieces. It feels *great*.

And that’s the position I’m in now, now that I’m at the top layer: code that I wrote a long time ago is finally getting *used*. The puzzle is coming together.

<p style="text-align:center">* * *</p>

Of course, I didn’t, and couldn’t, know *everything* in advance. I didn’t know I’d want Open Graph and Twitter images from web page data — but I was glad when I found that the code I’d already written was easy to extend.

<p style="text-align:center">* * *</p>

Since I have no commercial interest in Evergreen — since it’s free and open source — I can take all the time I need. One of the many advantages of this is spending more time writing unit tests than I used to.

There aren’t enough, yet — not even close; and there never are enough — but they do exist. Here, for example, are the <a href="https://github.com/brentsimmons/Evergreen/blob/master/Frameworks/RSParser/RSParserTests/HTMLMetadataTests.swift">tests for HTML metadata parsing</a>.

And when I find a bug I add a new test: for example, the feed type detector was not detecting <a href="https://www.natashatherobot.com/feed/">Natasha the Robot’s feed</a> as RSS. So I fixed the bug and [added a test](https://github.com/brentsimmons/Evergreen/blob/master/Frameworks/RSParser/RSParserTests/FeedParserTypeTests.swift).

<p style="text-align:center">* * *</p>

From the now-it-can-be-told department… a couple years ago, in November 2015, I collected a <a href="http://inessential.com/2015/11/16/blogs_by_women">list of blogs written by women</a> that would be “of interest to Mac/iOS developers, designers, and power users.”

This was for Evergreen. When I was working on NetNewsWire, the default feeds were all, or almost all, written by men. For Evergreen I wanted to fix that, and I also wanted to create a larger feed directory that was inclusive. (Here’s the <a href="https://github.com/brentsimmons/Evergreen/blob/master/Evergreen/FeedList/FeedList.plist">plist</a> for the directory. It still needs a bunch of work.)

If you have feeds to suggest, please do a pull request. Or send me a note on Twitter via <a href="https://twitter.com/evergreen_mac">@evergreen_mac</a>.

<p style="text-align:center">* * *</p>

I just started working on syncing via [Feedbin](https://feedbin.com/). It’s what I use, and syncing is necessary. It’s likely that 1.0 will ship with just Feedbin syncing, though, and I’ll add other systems in follow-up releases.

Also: I just got a new iPad Mini which travels to and from work with me. I didn’t expect to love this device so much! So now I’m thinking of doing Evergreen for iOS after all. (Also open source, as part of the same project.)

<p style="text-align:center">* * *</p>

It gratifies me to see my friends working on open web stuff. <a href="http://scripting.com">Dave Winer</a>, of course, is always on the ball. Daniel just released MarsEdit; Manton is working on <a href="https://micro.blog">Micro.blog</a>.

This is a political act, and, I think, fundamentally conservative: it wants to preserve what’s great about the web, and it recognizes that concentrations of power are bad things.

Power should be distributed to the individuals, not hoarded by large companies and governments that have their own interests in mind, which match ours purely by coincidence from time to time.

Next year may be a horrible year for a whole bunch of reasons, but it may also be a year where the open web fights back. Evergreen wants to help.
