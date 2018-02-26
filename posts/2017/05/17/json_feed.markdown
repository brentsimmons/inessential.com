@title JSON Feed
@pubDate 2017-05-17 13:22:14 -0700
@modDate 2017-05-17 13:30:12 -0700
I was hesitant, even up to this morning, to publish the <a href="https://jsonfeed.org/version/1">JSON Feed spec</a>.

If you read Dave Winer’s <a href="http://scripting.com/2017/05/09/rulesForStandardsmakers.html">Rules for standards-makers</a>, you’ll see that we did a decent job with some of the rules — the spec is written in plain English, for example — but a strict application of the rules would have meant not publishing at all, since “Fewer formats is better.”

I agree completely — but I also believe that developers (particularly Mac and iOS developers, the group I know best) are so loath to work with XML that they won’t even consider building software that needs an XML parser. Which says to me that JSON Feed is needed for the survival of syndication.

I could be wrong, of course. I admit.

#### Feed Reader Starter Kit

See my <a href="https://github.com/brentsimmons/RSXML">RSXML repository</a> for Objective-C code that reads RSS, Atom, and OPML. I’ve done the work for you of supporting those formats. Go write a feed reader! Seriously. Do it.

I planned to have a JSON Feed parser for Swift done for today, but other things got in the way. It’s coming soon. But you probably don’t actually need any sample code, since JSON is so easy to handle.

#### Feedback so far

Feedback has been interesting so far. Some <a href="https://github.com/brentsimmons/JSONFeed">questions</a> on the GitHub repo need answering.

Some people have said this should have happened ten years ago, and other people have said that they hate how developers jump on the latest fad (JSON).

And some people really like the icon:

<img src="http://jsonfeed.org/graphics/icon.png" height=70 width=70 />

#### Microformats

One of the more serious criticisms was this: why not just support the <a href="http://microformats.org/wiki/hatom">hAtom microformat</a> instead? Why do another side-file?

My thinking:

My experience as a feed reader author tells me that people screw up XML, badly, all the time — and they do even less well with HTML. So embedding info in HTML is just plain too difficult. In practice it would be even buggier than XML-based feeds.

And there are other advantages to decoupling: a side-file can have 100 entries where there are only 10 on an HTML page, for instance. A side-file can have extra information that you wouldn’t put on an HTML page. And yet, despite the extra information, a side-file can be much smaller than an HTML page, and it can often be easier to cache (since it’s not different based on a logged-in user, for instance).

Microformats sounds elegant, but I don’t prize elegance as much as I value things that work well.
