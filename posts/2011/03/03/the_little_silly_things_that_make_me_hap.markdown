@title The little silly things that make me happy
@categoryArray NetNewsWire
@pubDate Thu Mar 03 14:40:17 -0800 2011
@modDate Thu Mar 03 14:52:10 -0800 2011
For a while during development of NetNewsWire Lite 4.0, the BBC was a default feed.

But I couldn’t stand the way the favicon looked — I figured there was no way I could ship it as a default feed, given how the favicon looked. It looked like this:

<img src="http://inessential.com/images/blurry_bbc_favicon.png" alt="Blurry BBC favicon" height="15" width="20" />

Yuck, right?

But something about that just didn’t seem right. There’s no way the BBC would have knowingly created such a rough-looking favicon. It’s the <em>BBC</em>, after all, not Bob’s Burger Cabana.

So I inspected the favicon, opened it in Preview. And it turns out it had two representations, one at 32 x 32 and one at 16 x 16. My code was naively just scaling down the 32 x 32 version, hence the blurries.

I’m not a graphics expert. I know some people who are. But I figured this one out on my own! (Hint: ImageIO.framework.)

So I ended up getting the non-blurry version, and it looked so much better.

<img src="http://inessential.com/images/bbc_non_blurry.png" alt="Non-blurry BBC favicon" height="20" width="222" />

<h4>Postscript</h4>

Then I deleted it as a default feed anyway.

But then I noticed that the favicon is blurry in Safari too.

<img src="http://inessential.com/images/bbc_blurry_safari.png" alt="Blurry BBC favicon in Safari" height="33" width="198" />

The Safari team does fantastic work. I love the browser. (And WebKit.) And I mean absolutely no disparagement.

But still, I was a little happy at this little thing — that I got the BBC favicon right. :)

<h4>Update</h4>

Turns out this was an issue in Camino too. <a href="https://bugzilla.mozilla.org/show_bug.cgi?id=463725">Fixed</a>. (Via <a href="http://twitter.com/hendynz">Chris Henderson</a>.)
