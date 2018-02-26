@title Atom XHTML Content Considered Jerky
@pubDate 2014-04-21 13:36:09 -0700
@modDate 2014-04-21 14:01:19 -0700
Dr. Drang [writes about varying support](http://www.leancrew.com/all-this/2014/04/typepad-feed-frustrations/) for Atom’s <code>content type="xhtml"</code>.

I strongly disliked this part of the Atom spec.

The thing about this feature is that the HTML tags are included as naked tags in the XML. That is, they’re not escaped or placed in a CDATA section.

From the good doctor’s example:

<code>&lt;content type="xhtml" xml:lang="en-US" xml:base="&#8203;http://lancemannion.typepad.com/&#8203;lance_mannion/"></code><br />
<code>&lt;div xmlns="&#8203;http://www.w3.org/&#8203;1999/xhtml">&lt;p>&lt;em>Barnes &amp; Noble. Thursday. April 17, 2014. Six forty five p.m.&lt;/em>&lt;/p>…</code><br />
<code>&lt;/content></code>

Just look at it. This feature is a <em>giant</em> invitation to screwed-up feeds. The HTML — which is probably a blog post, typed by a human — has to be valid XML. People writing scripts to generate these feeds have to make sure they can turn that HTML into valid XML.

Feeds are already screwed-up often enough. This could only make it worse.

The second issue: how can a parser handle this? What an RSS/Atom parser really wants is everything between `<content>` and `</content>` as a string.

I remember writing this code for [NetNewsWire](http://netnewswireapp.com/), which still supports this feature. (I checked. I have no idea if they’ve touched my code or not.)

I’m going from memory, but I’m pretty sure this is what I did.

NetNewsWire used libxml2’s SAX parser, which meant it gets called when the XML parser encounters the beginning and end of a tag and when it encounters a range of characters. There was no easy way — that I know of; [correct me if I’m wrong](https://twitter.com/brentsimmons) — to tell the parser to treat everything inside a tag (`<content>` and `</content>`) as a string when there are XML tags inside that tag.

So I wrote the Atom parser to <em>rebuild</em> the HTML. It maintained a string and pushed stuff on it. If it encountered a tag and (optionally) attributes, it would create a string version and push it. When it encountered characters it would push those. When it encountered the end of a tag it would create a string version and push that. Once the `</content>` was reached then it had the entire string.

The end result was equivalent HTML, but not necessarily character-for-character the same, since little things like quote characters could change.

It worked. But boy was I coding <em>angry</em> that day.

PS Luckily I didn’t see this feature used very often. Still had to write the code, though.

PPS I still wonder if there’s an easier way. (Using a SAX parser. No way would I give up SAX. Performance and memory use considerations require SAX.)

PPPS For a great list of other ways feeds get screwed up, see [Brian’s Stupid Feed Tricks](http://inessential.com/2013/03/18/brians_stupid_feed_tricks).
