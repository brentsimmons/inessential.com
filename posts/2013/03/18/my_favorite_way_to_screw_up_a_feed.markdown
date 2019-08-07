@title My Favorite Way to Screw Up a Feed
@pubDate Mon Mar 18 17:56:35 -0700 2013
@modDate Mon Mar 18 17:56:35 -0700 2013
Since Brian worked on the server side, his list of <a href="/2013/03/18/brians_stupid_feed_tricks">Stupid Feed Tricks</a> didn’t include my very favorite feed screw-up.

A lot of hotels and similar offer wi-fi. When you open a page in your browser, it redirects you to their login page.

Those systems don’t differentiate between an http request made by a feed reader and an http request made by a browser. (Nor should they.)

But what happens is that you launch your reader and it gets a redirect for every single feed, to some kind of URL like <code>http://dumbhotel.com/register.aspx</code>.

Normally that would be fine. It’s just a redirect, and once you have actually logged in you can do a refresh in your reader and all’s well.

But!

No!

A bunch of these dumb systems redirect using a <em>permanent</em> redirect: they use <a href="http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html">301 instead of 302</a>.

When a feed reader gets a permanent redirect, it’s supposed to take that to mean: “Hey, the feed moved. It’s over here now. Save the new URL and use the new one from now on.”

And if you don’t do that in your reader, and your feed reader is popular enough, smart people who quite rightly care about proper behavior will call you out. You <em>have</em> to do that.

So you write your feed reader to do the right thing — and then one of your customers goes to a dumb hotel, opens their laptop, and their subscription list is wiped out. Every feed URL is replaced with <code>http://dumbhotel.com/register.aspx</code>. And now they can’t get their news, and they don’t know how to get it back.
