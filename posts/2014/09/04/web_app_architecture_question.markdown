@title Web App Architecture Question
@pubDate 2014-09-04 11:54:32 -0700
@modDate 2014-09-04 11:54:32 -0700
Vesper’s web app is small, just a couple thousand lines of code, and it’s split into two components: an API server and a website.

The API server handles syncing. It’s almost all JSON — it doesn’t serve any web pages.

The website is for verifying your email address and doing a password reset. It doesn’t talk to the database directly — it talks to the API server.

Both are Node.js sites.

I like this architecture mainly because my temperament pushes me toward modularity.

I like small, focused pieces that can be updated independently, as long as the API contract is upheld. I like that I can run as many instances I need of each component.

<p style="text-align:center">* * *</p>

But what if I were doing something larger?

Picture a hypothetical web app with the following components:

* Account management website (create account, login, email verification, password reset, profiles)

* API

* Background tasks — downloading tweets (let’s say), doing something interesting with the data

* Push notifications

* Main website (the UI for the app)

* Misc. website (marketing, privacy policy, about, help, support, etc.)

(Also assume a database and some kind of static file storage.)

How would you organize this?

My first thought is that these are all separate apps. But that’s just my reflex — it’s not necessarily the right way to do it.

<p style="text-align:center">* * *</p>

If they’re separate apps, then there are issues of code sharing. A simple example: each of the three websites should probably have the same navigation bar at the top. I can’t change it once — I have to change it three times.

Maybe that’s not the worst thing, and I’d put up with that in order to get the other benefits of modularity. But it gets worse: each website also needs to be able parse an authentication token cookie and decide if it’s valid or not and who it refers to.

Things like that could be solved via the API server — pass the token to the server and get a response back (valid, invalid, expired). But that adds latency to the system (and I’m a speed freak), and there is still *some* duplicated code (the code that calls the API server).

Okay. So the websites really need to be just one website. That gives us this:

* Website

* API

* Background tasks

* Push notifications

Question: can the website talk to the database? If not, then it has to go through the API server, which adds latency. If it can, then it's duplicating code that the API server knows about.

The same question could be asked about the background tasks and push notifications. Do they go through the API or, potentially, duplicate code from the API?

To get rid of latency imposed by API calls, and get maximum code-sharing and no code duplication, I end up with this:

* One big app with everything in it

Which goes against my grain.

Might as well use <a href="http://rubyonrails.org">Rails</a> or <a href="https://www.djangoproject.com">Django</a> at that point, right?

<p style="text-align:center">* * *</p>

Does JavaScript in the browser change things?

Consider the navigation bar that has to be the same across websites. If this is built in the browser, built by JavaScript that exists in one downloadable, static file somewhere, then I’ve eliminated code duplication.

(Let’s assume I don’t care about browsers with JavaScript turned off and I don’t care about browsers with poor standards support.)

At that point the three different websites could just be JavaScript apps which call the API server. The server components of those websites wouldn’t need to talk to the API server or to the database at all.

So, for fetching and updating data, instead of browser > website server > API server > database, we’d have browser > API server > database. Which sounds much better.

Are we at the point where this is really feasible and secure?

Also, does this just mean trading one big framework (Rails, Django) for another one (<a href="http://backbonejs.org">Backbone</a>, <a href="https://angularjs.org">Angular</a>, <a href="http://emberjs.com">Ember</a>), with the added disadvantage that the user has to *download* the framework? (Is that really a good idea given that many people might be on phones with spotty connections? Maybe those frameworks aren’t as heavy as I imagine.)

<p style="text-align:center">* * *</p>

Perhaps the trade-offs in the choice of monolithic vs. modular just balance out and don’t point to a clear better practice. In which case the answer would be: go with whichever I prefer, and deal with the challenges of that approach as they come up.

But I can’t help but think that maybe they *don’t* balance out, and that using something like Rails or Django is actually the best call for a web app like this, and that going with my personal preference for modularity would mean a lot of standing on my head while cleaning the house.

(Well. This is all hypothetical anyway.)

What would <em>you</em> do?
