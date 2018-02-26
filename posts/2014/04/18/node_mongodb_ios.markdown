@title Node + MongoDB + iOS
@pubDate 2014-04-18 10:34:59 -0700
@modDate 2014-04-18 10:36:09 -0700
A two-part tutorial from Michael Katz is a good place to get started writing services. Node makes a great API server. And it’s fun.

[How To Write A Simple Node.js/MongoDB Web Service for an iOS App](http://www.raywenderlich.com/61078/write-simple-node-jsmongodb-web-service-ios-app)

[How to Write An iOS App that Uses a Node.js/MongoDB Web Service](http://www.raywenderlich.com/61264/write-ios-app-uses-node-jsmongodb-web-service)

The tutorials use MongoDB. I haven’t had a good reason for a NoSQL database myself lately — but my early career, back in the ’90s, was all about schema-less databases, and I have a major soft spot for them.

(I’m digressing now.)

Frontier’s database was a hierarchy of tables. Each table could contain anything, including other tables — including even your scripts.

To run a script named myScript inside the bar table which was inside the foo table, you’d write foo.bar.myScript(params).

If that script took a string as a parameter, say, you could use a local variable or reference any string anywhere in the database: myApp.data.settings.username, for example. This was all presented with a user interface, navigable and editable.

I haven’t seen a database like that anywhere else since then. So easy and intuitive. Great for productivity. (It was within this laboratory that such things as templated and scripted websites, blogs, RSS, OPML, and XML-RPC were invented and/or fleshed-out.)
