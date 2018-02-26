@title On Fixing that NSNull Crasher in Overcast
@pubDate 2017-10-10 16:08:04 -0700
@modDate 2017-10-10 16:12:47 -0700
I don’t normally head home after lunch, but today I was on the bus going back to Ballard, about to open iBooks on my phone and get back to reading <a href="https://www.amazon.com/Caledonian-Gambit-Novel-Dan-Moren/dp/1940456843">The Caledonian Gambit</a> (which I’m thoroughly enjoying), when I decided to check Twitter first — and saw Marco’s tweet about <a href="https://twitter.com/marcoarment/status/917852761873637376">Overcast’s oldest crash</a>.

I’ve written before about how I love fixing crashing bugs. Partly because I’m adamant that an app should, at a minimum, keep running — and also because it’s fun detective work. (I’ve even written a series of blog posts on <a href="http://inessential.com/hownottocrash">how not to crash</a> in the first place.)

So I took this one as a challenge. Here’s how I figured it out:

* The exception reported `[NSNull doubleValue]: unrecognized selector`. Now, `NSNull` is a stand-alone code smell: there’s hardly ever a time where it should be used. Well, there was that one weird thing with the kerning a long time ago, but that’s about it. This crash is probably not that.

* Then I looked at the backtrace and saw `-[NSRTFWriter writeKern]`, and then I looked a little further and saw that an `NSAttributedString` was being exported to RTF, and, furthermore, `writeKern` probably *is* writing out the kerning attribute, which was set to `NSNull`. `writeKern` was expecting an `NSNumber`. So that was it.

I <a href="https://twitter.com/brentsimmons/status/917856551989166080">replied</a>:

>The kerning attribute is NSNull. That used to be the way to specify use font-specified kerning.

And then Marco <a href="https://twitter.com/marcoarment/status/917859334499037184">found the bug and fixed it</a>.

<p style="text-align:center">* * *</p>

This is a story about experience and luck, not brains. It’s just that I’ve been working with these APIs for a long time.

Here’s the story behind setting `NSKernAttributeName` to `NSNull`. Back in the iOS 6 days, when <a href="https://twitter.com/gruber">John</a> and <a href="https://twitter.com/dwiskus">Dave</a> and I were working on Vesper — which used a custom font, Ideal Sans — we noticed that the kerning was fucking awful. We obviously couldn’t ship it like that. We had to either figure out how to fix the kerning or switch to the system font — which would have been heart-breaking, since Ideal Sans was so perfect for this app.

So I searched around until I found that there was a little bit of magic: in our `NSAttributedString`s, we needed to set `NSKernAttributeName` to `NSNull` to get the font-specified kerning. I tried it — and it worked! We were able to ship with Ideal Sans.

(Here’s a <a href="https://github.com/brentsimmons/Vesper/search?utf8=✓&q=NSKernAttributeName&type=">search in Vesper’s code base</a> for that attribute.)

I don’t know if this bit of magic is still needed these days. Hopefully not — because 1) it’s weird to have `NSNull` have a meaning like this, and 2) `NSRTFWriter` doesn’t know to expect an `NSNull` instead of an `NSNumber` (this should get filed as a Radar).

I no longer remember exactly where I ran across that bit of magic. Memory tells me what it was a slide from a <a href="https://twitter.com/jamesdempsey">James Dempsey</a> talk somewhere, though I can’t seem to find it right now.

Anyway. This bug was fixed because years ago I was working with type nerds (and I am one myself), and because of James.

Fixing crashing bugs takes a village.
