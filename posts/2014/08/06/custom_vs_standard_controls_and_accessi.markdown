@title Custom vs. Standard Controls and Accessibility
@pubDate 2014-08-06 14:28:15 -0700
@modDate 2014-08-06 14:37:38 -0700
(Apple folks can look at <a href="rdar://17927379">rdar://17927379</a>.)

I’ve written a couple times recently about wanting to use standard controls instead of custom controls — but we have a bunch of cases where we need to use our app’s embedded font, which doesn’t go well with the system font, and most standard controls don’t let you use a font other than the system font.

Going custom is more work, yes, and more to maintain. But there’s another aspect, easily overlooked: standard controls come with built-in accessibility features, and you need to roll your own with custom controls.

Which means it’s even *more* work than expected. And it’s a good bet that Apple’s ace accessibility teams have done a better job than I will.

So I filed a Radar asking for the ability to set the font (via attributedText or other means) on standard controls, so we can take advantage of the great work Apple has already done. It’s in nobody’s interest that we go custom.

<p style="text-align:center">* * *</p>

I never really thought about accessibility that much until one day in 2003 when a NetNewsWire user sent me and Sheila an audio recording of what it was like to use the app. And, because NetNewsWire used standard controls exclusively — or lightly customized, but not from-scratch — it just worked. <em>It was so cool</em>. I hadn’t done a thing except to use AppKit as intended, and this user had an app that worked wonderfully for them.

I’ve grown even more attached to the issue of accessibility later as I came to understand it’s not about just one thing — it’s about a range of different things. And I can see it in my own life. At age 46 I’ve started to get far-sighted, and it’s difficult to read some text on my iPhone.

And I’ve been <a href="http://inessential.com/2009/10/29/vaccines">near-sighted since third grade</a> — *terribly* near-sighted. With my contacts out I have to hold a screen so close to my face that, even on a retina display, I can see the pixels. I have to close one eye. I have to physically *move* an iPad to read text at the bottom of the screen, since that distance is farther than I can see.

My case is easily manageable — but still, it means that accessibility is for me too, not just some people I haven’t met.
