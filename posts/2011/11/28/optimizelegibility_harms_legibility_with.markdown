@title optimizeLegibility Harms Legibility with Chromium on Linux
@pubDate Mon Nov 28 17:53:13 -0800 2011
@modDate Mon Nov 28 17:56:59 -0800 2011
I’ve heard from a number of people that the text rendering for this site was messed up when using Chromium on Linux. It looked like this:

<div style="text-align:center"><img src="http://inessential.com/images/optimizeLegibility_Chromium_bug_shadowed.png" width="248" height="89" alt="Screen shot showing messed-up text rendering" /></div>

I did some research, including installing the latest Ubuntu and Chromium in VMWare. I saw the bug too.

Eventually I found this <a href="http://code.google.com/p/chromium/issues/detail?id=96936">bug</a> on the Chromium bug tracker. Though the bug is specific about bold fonts and Microsoft fonts, it sounds to me as if the issue was with a line in my CSS: <code>text-rendering: optimizeLegibility</code>.

So I removed that line from the CSS for this site. I added a little JavaScript in the page header to check for Chromium — and, if not Chromium, then it does <code>document.body.style.textRendering = "optimizeLegibility";</code> to set the style. (I still need to do a comparison to make sure it’s working correctly. I’m not even a novice when it comes to JavaScript.)

I have a few theories as to why the bug is not more widely-noticed:

1. It may be that few sites use <code>optimizeLegibility</code> so far.

2. The display would fix itself if you refreshed the page. My guess is that a redraw/reflow would fix the bug, and most sites have something — an image, script, iframe, something — that would trigger at least one redraw or reflow, and so the bug was largely hidden. But this site is simple enough that it wouldn’t hide the bug.

3. It may be that the bug appears only with certain fonts.

Obviously, some combination of the above is possible. (Or something else I haven’t thought of.)

My point: if you use <code>optimizeLegibility</code> on your site, it’s a good idea to test with Chromium on Linux.
