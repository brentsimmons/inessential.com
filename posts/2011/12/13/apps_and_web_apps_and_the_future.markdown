@title Apps and web apps and the future
@pubDate Tue Dec 13 12:03:39 -0800 2011
@modDate Tue Dec 13 14:24:04 -0800 2011
Dave Winer: <a href="http://scripting.com/stories/2011/12/13/whyAppsAreNotTheFuture.html">Why apps are not the future</a>:

>The great thing about the web is linking. I don’t care how ugly it looks and how pretty your app is, if I can’t link in and out of your world, it’s not even close to a replacement for the web.

Let’s set aside one thing right away. The browser is an app. Text editors, outliners, and web servers are apps. And, without them, there’s no web at all.

Somebody has to write these things. That implies APIs and more tools that are also apps. It implies an entire ecosystem of apps that are absolutely vital to the web.

I think Dave is talking more specifically about the kind of apps we download from the Android and iOS app stores — apps like Instagram. The difference between these apps and a web app are:

1. They require downloading: the apps don’t live at a URL.

2. The user interface uses native code and controls rather than HTML (for the most part).

3. In the case of the iOS and Mac App Stores, those apps are reviewed before they’re posted.

4. You can’t (usually, and not easily) link to a specific piece of content in these apps. (There are exceptions, yes.)

#### Jeff Croft on the web

In A List Apart’s <a href="http://www.alistapart.com/articles/what-i-learned-about-the-web-in-2011/">What I Learned about the Web in 2011</a>, Jeff Croft writes:

>The most important thing I learned about web design and development in 2011 is that more and more, the “web” is APIs and services, rather than sites, apps, and pages rendered in web browsers. Take Instagram: it’s one of the most popular services on the “web” and the entire experience is controlled not by some HTML pages, but rather by an iPhone app.

#### Apps are the future and web apps are the future

I think we’ll have both with us for a long time.

There’s one simple reason that should suffice: *some developers love writing apps and some love writing web apps, and some love writing both*.

This means that people will keep making both kinds of apps. One thing we’ve learned about developers is that economics matters, but love matters too, and many developers will make the kind of software they love to make.

Me, I’m the kind who loves writing both. I’m doing some web work at the moment — it’s been about 10 years since I worked on a web app, and I’m totally excited. It’s fun. The technology has changed so much since then and I’m having a blast. (Today I’m doing my first work with <a href="http://sass-lang.com/">Sass</a> and <a href="http://compass-style.org/">Compass</a>.)

#### Some questions

How could you make <a href="http://instagr.am/">Instagram</a> without a native client? Is it possible to do those image transformations via JavaScript?

Can you link to Instagram-taken pictures?

If I’m running <a href="http://www.omnigroup.com/products/omnifocus/">OmniFocus</a> on my iPhone, and it syncs over the web — do I want anybody to link to my OmniFocus to-do items? Or to my <a href="http://tapbots.com/software/weightbot/">WeightBot</a> stats? To my notes that I edit with <a href="http://www.secondgearsoftware.com/elements/">Elements</a> and keep in a folder on <a href="https://www.dropbox.com/">Dropbox</a>? To my direct messages that go over <a href="http://en.wikipedia.org/wiki/IMessage">iMessage</a>?

When publications make such truly <a href="http://inessential.com/2011/11/22/the_pummeling_pages">excruciatingly awful websites</a> as they do, should I not read them in <a href="http://zite.com/">Zite</a> or <a href="http://flipboard.com/">Flipboard</a> or <a href="http://www.instapaper.com/">Instapaper</a> instead?

#### Two layers of web

One layer of the web is the http web: the web of <a href="http://httpd.apache.org/">Apache</a>, <a href="http://wiki.nginx.org/Main">Nginx</a>, <a href="http://nodejs.org/">node.js</a>, <a href="http://couchdb.apache.org/">CouchDB</a>, <a href="http://www.mysql.com/">MySQL</a>, <a href="http://www.json.org/">JSON</a>, <a href="http://cyber.law.harvard.edu/rss/rss.html">RSS</a>, <a href="http://dev.opml.org/">OPML</a>, <a href="http://xmlrpc.scripting.com/">XML-RPC</a>, and <a href="http://en.wikipedia.org/wiki/Representational_state_transfer">REST</a>.

That’s the web of backend databases and APIs. That web powers both apps and web apps.

The higher level of the web is the web of HTML, CSS, and JavaScript. That’s the web that runs in a browser (and in web-views in apps). That’s the web that will always lag native code in some respects but that has strengths that native code doesn’t have.

In the past, that higher level of the web pushed most of its work to the server side. But today’s advancements (<a href="http://en.wikipedia.org/wiki/HTML5">HTML5</a>, <a href="http://www.css3.info/">CSS3</a>, <a href="http://twitter.github.com/bootstrap/">Bootstrap</a>, <a href="http://documentcloud.github.com/backbone/">Backbone.js</a>, <a href="http://jquery.com/">jQuery</a>, and so on) are about pushing that work to the client side — as apps already do — and accessing the server via (usually RESTful JSON) APIs. Those APIs can be used by both web apps and apps.

I like this. A lot. I like the cleanest-possible separation between backend and presentation. I like language-agnostic APIs and APIs that don’t care at all about how the data is presented. That’s just good architecture.

#### The future is tangled

If I had to choose one or the other — if I had some crazy power but I <em>had</em> to wipe out either native apps or web apps — I’d wipe out native apps. (While somehow excluding browsers, text editors, outliners, web servers, and all those apps we need to make web apps.)

That’s not the case, though. Nothing has to get wiped out.

I think instead that we’ll see a more tangled future. Native apps will use HTML, CSS, and JavaScript more. Web apps will appear more often on smart phones as launchable apps. Native apps will support linking in and out more. Web apps will move more processing to the client — they’ll be written more like native apps. (Is Twitter an app or a web app? It’s already getting tangled.)

There will be times when you won’t know which kind of app you’re looking at or how to categorize it. I think that’s very cool.

There are multiple tracks of evolution, but those tracks are heading to the same city. And there are plenty of hobos like me that love hopping trains — for fun, to satisfy curiosity, to tell stories and hear stories — on the way there.
