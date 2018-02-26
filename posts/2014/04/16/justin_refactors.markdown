@title Justin Refactors
@pubDate 2014-04-16 10:20:35 -0700
@modDate 2014-04-16 10:20:35 -0700
Justin Williams: <a href="http://carpeaqua.com/2014/04/16/refactoring-in-the-cloud-notifications/">Refactoring in the Cloud</a>:

>Given that I’m not a fan of the C# threading model currently implemented, the amount of code used to power something that’s relatively simple, and the homegrown nature of many of the push wrappers we’re using, I made the decision to rewrite this portion of Glassboard’s architecture using Node.

Justin’s use of Azure is quite different from mine. Glassboard is more complex than Vesper syncing, which should be no surprise.

(If you think about it, you realize that Glassboard does syncing, but it’s silly to call it that because it’s a natural part of what’s expected of a group messaging app.)

Vesper’s architecture is smaller. There are two main components: an API server (Node.js Mobile Services app) and a reset-password site (Azure web site, also Node.js). There are no architecture-level refactorings for us to do at this point.

We’re at about 2,000 lines of server-side code. Small.
