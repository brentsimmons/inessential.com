@title 30 Minutes To Sync
@link http://atomicbird.com/blog/icloud-complications-part-3
@pubDate Tue May 07 12:21:20 -0700 2013
@modDate Fri May 10 19:54:18 -0700 2013
Tom Harrington continues his series of <a href="http://atomicbird.com/blog/icloud-complications-part-3">posts on iCloud and Core Data</a>.

><strong>I’ve seen <code>addPersistentStoreWithType:&#8203;etcetera:</code> block for 30 minutes.</strong> And keep in mind, <em>this is when iCloud is working normally</em>. This is not an error condition, this is “working as designed.”

He suggests a solution: using two separate databases, one for normal use and one just for syncing, with custom code that shuttles data between the two.

That solution points to what bothers me about the whole thing, which is that this is all too tightly-coupled. Ideally your storage system and syncing system are not the same thing, and you could swap out one for another.

This would allow for flexibility and efficiencies that you can’t get when you just say “here’s my database; please sync it, iCloud.”

#### Apple and Backend Services for Apps

Imagine Apple announced something that worked like this:

- You go to a website somewhere at apple.com and set up a backend for your app.

- You create a database for it and a custom https API. You might have to write some code — but it would be in a popular scripting language, nothing weird. All this with a browser-based UI.

- Apple provides a client framework for making calls to the server.

- Authentication is completely taken care of — the system uses iCloud credentials, and your app doesn’t have to do anything. (It just knows if you’re authenticated or not.) In your app a user never has to sign in or create an account or anything like that.

- Everything Apple stores is automatically encrypted. Apple’s server takes care of encrypting/decrypting automatically, so your code (in the client or on the server) never has to deal with that.

- Apple’s system provides the ability run periodic tasks (like polling Twitter, App.net, or RSS feeds).

This would be more general than just a syncing solution, but you could use it just for syncing. Or you could add more sophisticated backend services. (You could write an RSS reader with this or something social like Glassboard.)

It would have to cost money, of course.

And you’d have to write code; you’d have to design your syncing system. But it would give you abilities you don’t have with iCloud Core Data syncing, and it would decouple your database and syncing, which is the right way to go.

I’ve mentioned <a href="http://www.windowsazure.com/ios">Azure Mobile Services</a> before, which I like because it’s in spitting-distance of an idealized Apple service. I would go so far as to suggest that Apple and Microsoft should partner to provide this service. Play to each company’s strengths.

(Disclaimer: Mobile Services paid me to do some videos for them and has sponsored my podcast.)

#### Syncing is only part of the future

Even if Apple works out syncing — somehow — that’s just not enough. That just gets us to where we should have been in 2008. The future belongs to apps with more sophisticated services.

And the future belongs (in part) to whoever provides those services. If you’re an iOS or Mac developer, you’d like it to be Apple.

Here’s what should worry folks at Apple: that Google provides something like the above for Android developers. Google obviously has the expertise, and it wants to make Android more attractive to developers.

(Yes, there’s Google App Engine, but I’m imagining something easier.)

Or, put another way: the backend system will become nearly as important as the UI frameworks, and plain-old-syncing isn’t enough.
