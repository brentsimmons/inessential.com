@title IAC on iOS
@pubDate 2014-04-18 11:14:22 -0700
@modDate 2014-04-18 15:58:30 -0700
Check out [GCDWebServer](https://github.com/swisspol/GCDWebServer). (Via [iOS Dev Weekly](http://iosdevweekly.com/), which you should subscribe to.)

GCDWebServer is an embeddable and lightweight http server for Mac and iOS. On iOS it runs as a background task — it keeps running even when your app isn’t in the foreground.

Picture this: app X wants to send some data to app Y.

App Y is running GCDWebServer, so app X wraps up the data as JSON and talks to app Y via http. Just as if it were talking to some server on the web, only it’s a local app.

<i>Update 4 pm</i>: [Or not](https://developer.apple.com/library/ios/technotes/tn2277/_index.html). I’m not sure it’s possible, or maybe just not allowed, to keep a network server running when the app is in the background.
