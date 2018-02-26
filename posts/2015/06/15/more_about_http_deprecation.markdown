@title More About http Deprecation
@pubDate 2015-06-15 12:00:53 -0700
@modDate 2015-06-15 12:01:39 -0700
Dave Winer writes about http deprecation in <a href="http://scripting.com/2015/06/15/thePeoplesBrowser.html">The People’s Browser</a>.

And I’ve thought more about it in the context of writing Mac and iOS apps. Let’s consider a few apps I’ve worked on in my career:

NetNewsWire: an RSS reader that connects to any site with an RSS feed, no matter how that feed is served (http or https).

MarsEdit: a blog editor that connects to any blog with an external API, no matter how that API is served (http or https).

Glassboard: a private group messaging system.

Of these, only Glassboard would fit in an https-only world. Since we controlled the server, and since privacy and security were hugely important, requiring https would be no problem. (And of course we did use https.)

The problem is the other two apps. They all rely on the open web rather than servers controlled by the app writer. And it would be unacceptable to limit those apps to https only.

Let’s also consider my two secret-project Mac apps. Both of them need http access — they’re not limited to servers that I (or some corporation) control.

Since neither app will be sandboxed, I’ll be able to do this without Apple’s approval. My concern, of course, is that this situation won’t last. (It already means that there couldn’t be iOS versions of my secret-project apps — at least not without Apple granting an exception, which may be temporary.)

I’m totally on board with defeating the ability of the NSA and your internet provider and everybody else from snooping. I *hate* this snooping business — it’s anti-American and it makes me sick to my stomach for the future.

But I also know that the web isn’t going to switch to https quickly or completely. It’s *expensive*. To cut off http is to cut off the arms of the body of free speech.
