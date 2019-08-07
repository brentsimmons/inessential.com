@title A Clarification Regarding Web Services and Control
@pubDate Thu Mar 28 10:33:59 -0700 2013
@modDate Thu Mar 28 10:49:15 -0700 2013
Responding to <a href="/2013/03/27/why_developers_shouldnt_use_icloud_sy">yesterday’s post</a>, a number of people pointed out to me that it sounded weird if one minute I suggest checking out Azure <a href="http://www.windowsazure.com/ios">Mobile Services</a> and the next minute tell developers they should take control of their app’s web services.

I meant no contradiction, but I could have explained better.

When creating web services, you should consider high-level systems, low-level systems, and everything in between, and figure out what makes sense for you.

Here are some — not necessarily all — of the things to consider when choosing:

* Does it support iOS, Android, and browser-based apps? (Knowing that you may — may — want to move beyond just iOS.)

* Can you create a social component?

* Can you add additional services — push notifications, feed-polling, sending email, whatever — to the system?

* Can you get aggregate data and learn how people use your app?

* Perhaps most importantly: is it possible to migrate to something else (even if takes some work)?

The answer is yes to all of these for Mobile Services. (While the answer is no to all of them for iCloud syncing.)

The answer is also yes if you want to work at a low level — it’s yes if you get a virtual server on <a href="http://www.linode.com">Linode</a> and run Ruby on Rails and MySQL.

And it’s also yes if you work at a medium level and deploy apps using services like <a href="http://www.heroku.com">Heroku</a>, <a href="https://www.engineyard.com">Engine Yard</a>, <a href="http://aws.amazon.com">Amazon</a>, and <a href="https://developers.google.com/appengine/">Google App Engine</a>.

At some point you have to outsource some things, right? You’re not going to build your own server machine that runs your own operating system in a data center you constructed with hammers and saws that you made.

So you choose what makes sense. And if it can be a high-level system, that’s cool — it will probably save you time and be easier to maintain. But you might have good reasons to choose something medium or low level, and that’s cool too.

The key is this: <em>you need control of the data</em>.

iCloud Core Data syncing is, once again, completely opaque and outside your control. It fits <em>none</em> of the criteria listed above.
