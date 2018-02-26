@title BSSAXTweetParserDemo
@categoryArray Cocoa-Development
@pubDate Thu Jun 03 21:09:58 -0700 2010
@modDate Thu Jun 03 21:13:41 -0700 2010
I had reason to look at <a href="http://github.com/mattgemmell/MGTwitterEngine">MGTwitterEngine</a> today. It had been a while since I looked at it, and I was reminded that the libxml-based parser in there was originally based on my <a href="http://inessential.com/2008/04/15/libxml2_xmltextreader_on_macs">BSTweetParser</a> from a couple years ago. (Folks did a real nice job of improving it, of course.)

But I don’t do my XML parsing like that anymore. I still use libxml, but I use the SAX interface these days.

Here’s a new demo project — somewhat like the old BSTweetParser, but using SAX: <a href="http://ranchero.com/downloads/BSSAXTweetParserDemo.zip">BSSAXTweetParserDemo</a>. (It’s an Xcode project folder with source.)

I have no special unnatural love for SAX, like some <a href="http://shapeof.com/">people</a>, but it’s the best way to get both high performance and low memory use. (These days I <em>always</em> use SAX.)

<h4>Notes about the code</h4>

Twitter’s public timeline XML is very simple, so it makes a great demo. Easy to follow what’s going on.

SAX is event-based.

SAX means you don’t have to have the entire XML document in memory — you can pass it to the parser in chunks. This demo doesn’t do that, but my production code does. (Do you want to hold a 5MB XML document in memory on an iPhone? Nope.) Luckily, NSURLConnection makes this very simple. Don’t append data to build the response body — just pass each chunk to the parser and forget it.

The original BSTweetParser code allocated a ton of strings and dictionaries. This new code still has to allocate memory — but it allocates a whole lot <em>less</em> memory. This makes a giant difference on iPhones and iPads.

The original BSTweetParser code just turned everything into arrays, dictionaries, and strings. This new code is selective: it stores only what it wants to store, and it uses custom objects: BSTweet and BSUser instead of dictionaries. I recommend this when performance and memory use matter (as they always do on iPhones and iPads).

The comments in the demo code hint at, but don’t entirely demonstrate, the best way to parse a stream like a stream of tweets: don’t create a big array — instead, each time you have a new tweet, call some delegate to do something with it. No need to store the whole thing as an array and then process it — that uses too much memory. (But that’s exactly what the demo is doing. To keep the demo simple.)

This code not only does less memory allocation, it’s also more than twice as fast as the original BSTweetParser. (The two things are related, of course.) On my development machine, BSSAXTweetParser parsed the timeline in about 0.0008 seconds, while BSTweetParser did it in about 0.0017 seconds. (“Faster <em>and</em> less memory? Sold!”) (I bet the difference is way more dramatic on iPhones, but I built this is a Mac Foundation tool.)

You’ll probably realize fairly quickly what parts of the BSTweetParser class could be made an abstract class from which your real parsers would inherit.

There’s a bunch more code in BSSAXTweetParserDemo than in BSTweetParser. I prefer less code to more code almost as much as I prefer breathing to not-breathing. But that’s life — sometimes the faster and better thing takes more code.

I put this thing in the public domain. Use however and wherever.

In the tradition of all demos ever, there’s no error checking or handling.

When it comes to things like XML parsing on iPhones and iPads, the entire name of the game is <em>doing the least work possible</em>.

There are ways to make this even faster still.
