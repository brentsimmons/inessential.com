@title Dave on JavaScript Apps
@pubDate 2014-09-05 13:57:05 -0700
@modDate 2014-09-05 14:06:09 -0700
Dave Winer, <a href="http://scripting.com/2014/09/05/iWriteAppsInJavascriptInTheBrowser.html">I write apps in JavaScript that run in the browser</a>:

>I go to the &lt;script> section and start writing routines. Just as if I were going to run it from my desktop, which in a very real sense I am. It’s just that today my desktop exists mostly in my mind. Which is where it always has been.

I don’t think Dave is using any of the frameworks like Backbone, Ember, or Angular. (jQuery maybe? I don’t know.) He does use Bootstrap, I believe.

I like this approach. Part of me thinks those frameworks are overkill (even jQuery), and that writing regular-old JavaScript to do what you want is not that onerous a thing, and will make for leaner, better code. (Along the way you’d develop your own library, of course.)

But that’s just me — I like to minimize dependencies. And I don’t like the idea of a browser downloading 100K (or more) of code when it could be 10K. And I don’t like the idea of updating my code just because a framework made a breaking change but I need to upgrade because there’s also a security fix. (Would this happen? I don’t know. Could just be paranoia on my part.)

On the other hand, there really is something to be said for these frameworks. If they take care of the boring parts, and then just get out of the way and let me concentrate on the unique parts of my app, then that’s a win.

<p style="text-align:center">* * *</p>

Web apps make such an interesting contrast with iOS and Mac apps. With native apps, you use Xcode and the Cocoa frameworks, and that’s that. You might choose between Objective-C and Swift, and you might choose to use some open source libraries such as AFNetworking.

But those choices are few and relatively small compared to all the choices with writing web apps.

You could say that writing iOS and Mac apps is like living in a town where one company provides most of the jobs. (Sure, you could work at the diner, but all your customers work at this one company.)

And writing web apps is like living in New York City, where choice and contrast is everywhere, and sometimes A and B (and C and D) are all equally cool but different.

The web is the cosmopolitan environment.
