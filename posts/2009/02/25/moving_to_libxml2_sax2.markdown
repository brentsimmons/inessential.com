@title Moving to libxml2 SAX2
@pubDate Wed Feb 25 09:50:55 -0800 2009
@modDate Wed Feb 25 09:50:55 -0800 2009
There are two types of code I especially love writing: very high-level code that reads like human thought and low-level code that solves a specific problem.

(Aside: the problem with AppleScript is that it’s high-level like <em>speech</em> instead of high-level like <em>thought</em>. But people don’t speak programs, they <em>think</em> them.)

I’ve just about finished moving my XML parsers from libxml2’s <a href="http://xmlsoft.org/html/libxml-xmlreader.html">xmlReader API</a> to libxml2’s <a href="http://xmlsoft.org/html/libxml-SAX2.html">SAX2 API</a>. This would fall into the category of “low-level code that solves a specific problem.” So it’s fun. :)

#### Why make this move?

There are a couple main reasons to do this:

1. There’s a small memory leak in xmlReader, at least in the version of libxml2 that appears on Macs and iPhones. It’s not a <em>bad</em> bad leak — but every leak should be fixed.

2. The SAX2 parser can process XML in <em>chunks</em>. You can pass it part of a document, then the next part, then the next, until finished. This means you don’t have to have the entire document in memory — which is great if you’re downloading and parsing a large feed: each time you get additional data, you can pass it to the parser then release the data (that chunk). (None of NSXML* has this same capability.) This is obviously a good thing on iPhones, but not at all bad to have on Macs as well.

One drawback of libxml2’s SAX2 API is that it’s a C API. Which, for me, isn’t much drawback — I don’t mind C at all. (In fact, I like it for code like this.)

But still, my approach is to write a simple base class that handles the complex bits, then do sub-classes that are easy to write. It’s the thinnest of wrappers, using the guiding principle of not creating objects unnecessarily — but it’s enough of a wrapper to let me use Objective-C and Foundation data types.

#### For more info

If you’re interested in more about this, I recommend Apple’s XMLPerformance sample code. (Somewhere on the iPhone Dev Center.) It compares NSXMLParser and libxml2 SAX2.

#### Good for Macs too

There’s a third type of code I especially love writing: code that gets used in <em>all</em> my projects, all my iPhone and Mac software.

It’s cool how working on iPhone software has caused me (and lots of other Mac developers) to concentrate on memory use and performance in ways we haven’t had to for many years — which will also benefit our Mac apps.

#### PS You get to write a state machine

I was talking SAX with some local developers the other day. I hope <a href="http://gusmueller.com/blog/">Gus</a> won’t mind my reporting that he loves SAX, because “you get to write a state machine!”

Which to me is like saying, “You get to have your eyes slowly gouged out with moldy bananas!” And I <em>don’t like bananas</em>.

For anyone used to DOM parsers, SAX seems, at first, to be inside-out, backwards, <em>and</em> upside-down. Tesseract-y and vicious.

But you can wrap your head around it quickly, and, depending on what you’re processing, you may not have to deal with that much state at all. (The hardest thing I’ve had to do — which is easy, face it — is parse hierarchical OPML documents. A LIFO stack does the trick.)

Anyway, I’m just saying, don’t let Gus scare you off.

#### PPS Now I get to delete some code

I’m off to delete my old xmlReader API code. Now <em>that</em> is fun.

Part of me wonders if I went through all this just so I could use the delete key a bit. No. Couldn’t be.

Could it?
