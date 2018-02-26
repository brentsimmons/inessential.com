@title Brian’s Stupid Feed Tricks
@pubDate Mon Mar 18 14:25:00 -0700 2013
@modDate Mon Mar 18 17:43:25 -0700 2013
At NewsGator and Sepia Labs I worked with <a href="https://twitter.com/brianreischl">Brian Reischl</a>, one of the server-side guys. Among other things, he worked on NewsGator’s RSS content service, which reads n million feeds once an hour.

(I don’t know if I can say what n is. It surprised me when I heard it. The system is still running, by the way.)

Brian is intimately acquainted with the different ways feeds can be screwed up. So he posted <a href="https://docs.google.com/document/d/1cvq67iQpk2C7ufOsefsfKnGCXeUIv46NQHbnHkm8PtU/edit?usp=sharing">Stupid Feed Tricks</a> on Google Docs.

I quote the entire thing below for people like me who don’t have Google accounts. The below is all by Brian:

#### Stupid HTTP Tricks

1.	When the feed is gone/errored, publisher may still return a 200 OK but send an HTML page instead.
2.	Using permanent redirects for temporary errors. In one instance, all the Microsoft blogs had a temporary system error. All the feeds did a permanent redirect to the same system error page, and we updated all 40,000 feeds to point to that one URL. Whoops. 
3.	Using very slow or overloaded servers. It might take 60 seconds just to connect and send the request, another 60 seconds to first response byte, and so on. This can bog down your content retrieval. 
4.	Very slow responses, or responses that never actually complete (ie, you hang trying to read data essentially forever)
5.	Infinitely long responses. eg, feed server has an error and prints an error message in a infinite loop until something stops it. Hopefully it’s stopped by a check in your system, rather than consuming all the memory on your server.
6.	Sending back things that are not XML (eg, videos). It can help to check Content-Type and Content-Length headers, but sometimes they misidentify RSS as something else (eg, text/plain).
7.	Returning an HTML page containing HTML/Javascript redirects instead of using HTTP redirects.
8.	Infinite redirect loops.
9.	Long (but non-infinite) chains of redirects.
10.	Responding with 304 Not Modified if you send any If-None-Match/If-Modified-Since header, even if the feed has changed.
11.	Throttling your IP address. Some don’t tell you they’re throttling. Some provide Retry-After headers, but the HTTP status code can vary. eg, Twitter used to use their cutesy “420 Enhance Your Calm” response, then switched to “500 Internal Server Error”. Some use “503 Unavailable”. You’re mostly covered if you look for Retry-After headers in every non-success response.. 
12.	Redirecting (perhaps permanently) to a URL that’s already in your system. So now you either have a duplicate feed, or you have to update clients somehow. Note this can sometimes be legitimate, eg consolidating multiple feeds into one.

#### Stupid XML Tricks

1.	Any sort of XML well-formedness error you can think of. Missing closing tags, mismatched tags, bad escaping, not quoting attributes, missing root elements.
2.	Including unescaped HTML content inside a tag - which sort of works, except that most HTML isn’t XML-compliant.
3.	Putting in characters that are illegal in XML documents (eg, some non-printable characters that should be escaped, but aren’t)
4.	Declaring the document as ISO-8859-1 encoding, but actually using UTF-8, with some Arabic characters in it. 

#### Stupid RSS/Atom Tricks

1.	Missing any element you can think of. 
2.	Adding custom elements without namespaces.
3.	Using common extension elements without defining the namespaces (eg, using the common “mrss” namespace prefix for MediaRSS elements, without actually specifying that namespace anywhere)
4.	Not providing a GUID.
5.	Providing the same GUID for every post in the feed (eg, using the feed URL as the GUID)
6.	Providing the same GUID for every post, but changing each time you request the feed (eg, using the current date/time)
7.	Using a different GUID for each post, changing each time you request the feed (eg, generating an actual GUID each time the feed is requested)
8.	Not giving a PubDate
9.	Changing the PubDate on every retrieval.
10.	Changing the PubDate when a post is edited, rather than using a lastUpdated tag. 
11.	Putting a tiny number of posts in the feed (sometimes just one). These types then usually publish 10 articles in the space of two minutes, and wonder why you’re missing 9 of them. 
12.	Putting only one post in the feed, with a GUID that never changes. When there are new posts, just the title and description change. (I believe this was a bunch of Japanese newspaper sites.)
13.	Updating post content without changing the lastUpdated date (or not having one)
14.	Updating post metadata (eg, enclosures, MediaRSS extensions, etc) with or without changing the lastUpdated date.
15.	Treating their feed as append-only, so over time the feed grows without bound. eg, each request might pull back 10,000 posts covering the entire 8 year history of the feed.
16.	Specifying dates in whatever their language’s “Date.ToString()” spits out. eg, “Tuesday, March 31st, Year Of Our Lord Two Thousand And Twelve, 4:59 PM” 
17.	Not specifying timezones for dates (very common. It’s easy to just assume UTC, but note that can yield pubdates in the future).
18.	Specifying dates that are far in the past or future (anything up to thousands of years)
19.	Having the Link element point to another site. This is actually pretty common (eg, DaringFireball). This can be a problem depending on how you’re identifying individual posts, or if you’re trying to detect duplicates across feeds. 

#### Other Stupid Tricks

1.	Updating posts very frequently. Newspapers are very fond of this. In 4 hours they might change a post 12 times, by the end it might have nothing in common with the original article (completely different title, completely different body). Sometimes combined with not using lastUpdated, or just not changing lastUpdate. 
2.	Publishing updated posts as new posts, so you have 12 versions of the same post in the feed. 
3.	Occasionally giving you an two-week-old version of the feed for one or two requests. It looked like one server in a cluster had cached an old version and wasn’t updating it. (This was the New York Times back in ~2009. They might’ve fixed it by now.) 
4.	Adding posts very quickly. This is very common with feeds like the StockTwits stream, Twitter feeds (when that was allowed), the “all news” feeds from news organizations, etc. If you only check the feed every 60 minutes, you could easily miss something.
5.	Changing content literally every time you get the feed. eg, a feed that returns the current time in all the timezones, or the current weather for 20 different cities. 
6.	Putting out private data without requiring authorization of any sort. eg, a feed of all your GMail. This isn’t a problem until you provide search or other feed discoverability, and then people’s private data starts showing up. Then they get very angry. 
7.	Some places will publish a feed and then get angry that you use it, especially if you have ads in your reader. (name redacted before I get sued) got *very* bent out of shape over that back in ~2007.
8.	Providing feeds, but then also using robots.txt to say you can’t crawl it. So now do you violate the robots.txt, or not let your users subscribe to feeds because the publisher is a dipshit?
9.	Providing valid, but limited interest feeds. eg, search feeds (couches for sale in Portland on Craigslist!). Also lots of custom things like combinations from Yahoo Pipes (or whatever equivalent people come up with), bookmark/favorite feeds, etc. Can lead to lots of duplicate (or near duplicate) posts, and lots of feed retrievals that very few people care about.
10.	Publishers will routinely have 2-4 copies of the exact same feed. eg, one sourced from their site, and another republished through FeedBurner. Note: FeedBurner includes extension elements that tell you what the source feed and post were.
11.	Including malicious Javascript or HTML inside of the content in hopes of hacking your system. There was a test suite for this, unfortunately I don’t have the URL handy just now.

#### Random Notes

12.	You should think hard about canonicalization of URLs. Some parts of the URL can be case-sensitive (path and query) other parts can’t (protocol, host and post). Users (and webmasters) will absolutely use different upper/lower casing in different places.
13.	If you build a database index on FeedUrl, consider that 99% of them start with “http://”, which makes for a shitty index. Consider separating the protocol into its own column, and then indexing on the remainder of the URL. Alternatively, you could index on a hashed value of the URL. Theoretically you could have collisions, but in practice there are not that many feeds. 
