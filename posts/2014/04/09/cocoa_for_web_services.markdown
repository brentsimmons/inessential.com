@title Cocoa for Web Services
@pubDate 2014-04-09 11:58:31 -0700
@modDate 2014-04-09 12:50:03 -0700
Consider <a href="http://www.marco.org/">Marco Arment</a>’s software. You know him from Tumblr, Instapaper, The Magazine, and (coming soon) Overcast.

You may think of Marco as an iOS developer — but every single one of those apps is a web service.

And, furthermore, those web services do more than just provide syncing between iOS devices, though syncing is a component.

Here’s the lesson to learn: we’re no longer in the apps business. We’re in the apps-and-services business.

#### The problem with generic syncing

Generic syncing with Mac and iOS devices will never be as efficient as something you build yourself. It’s a super-hard problem to solve, but there are people and teams <a href="http://www.ensembles.io/">who’ve made progress on it</a>.

It <em>will</em> get solved to the point where lots of apps can adopt it without too much trouble.

But it’s not enough. If it’s easy, everyone does it, and it’s a baseline. Competitive apps will have better and more efficient sync — and they will have more than just syncing with Mac and iOS devices.

They’ll have additional services — which might mean support for other platforms (web, Android, etc.), publishing (as <a href="https://dayone.me/">Day One recently added</a>), social networking, content services, and so on. (It depends on the app.)

The cloud is more than just a file system. It’s data plus <em>code</em>.

#### Progress

Though there has been amazing progress in the web world in the last 10 years (while I was mostly ignoring it), we don’t have the equivalent of Cocoa for web services. I think it’s coming, though.

I don’t mean that we’ll write in Objective-C and host our services on Macs (though we might, and I’m aware that there was once a thing called WebObjects) — I mean that eventually we’ll have something that matches Cocoa in spirit.

Whatever it is will have these things in common with modern Cocoa:

* It will be very high level.

* It will solve all the common problems easily, via configuration.

* It will allow developers to concentrate on the parts that make their app unique — while still using rational APIs and design patterns encouraged by the framework.

* It will be customizable at every level.

* It will be fast and efficient — built for small teams making consumer apps rather than for enterprise.

#### An Example

An accounts system — with password-reset pages and everything else — is an obvious example. Let’s talk about something more complex.

A common issue for lots of apps is storing images and videos in the cloud and optionally publishing them. This means generating and storing images at different resolutions and transcoding video for different platforms.

It means serving the right size and format to the device or computer that asks. It means managing permissions — is this private to me or to a group, or is it public?

This is something you can solve using S3, Azure blob storage, or a file system somewhere. But to do so is to reinvent the wheel. This is exactly the kind of thing that should be solved once and made a part of a high-level web services framework.

#### Second Example

How many services are based on polling? Reading RSS and Twitter feeds, web pages, some APIs somewhere — and then parsing the results somehow and updating a database.

It’s another super-common pattern — and, again, the kind of thing that could be solved once. Give me an API that makes it easy to configure a download queue and add things to it. I’ll write a delegate method that parses the results of a download. Maybe there’s a second queue to update the database. And observers that determine who should get push notifications.

Sending a push would be as simple as providing some user IDs and the message to send — the service would use the right mechanisms for the right platforms for those users.

Seems obvious, right? Imagine writing web services the same way you write apps.

#### Who Will Get There First?

What I saw in <a href="http://azure.microsoft.com/en-us/develop/mobile/ios/">Azure Mobile Services</a>, which I use, is that they’re moving in that direction. It’s not there yet, and I think it will be a while before anybody has the whole thing. But the idea that there’s a higher level than deploying Node.js sites is absolutely correct.

I have *not* checked out everything else. Many people like <a href="https://parse.com/">Parse</a> (Facebook liked them <a href="http://techcrunch.com/2013/04/25/facebook-parse/">enough to acquire them</a> last year).

Another one people like, <a href="http://helios.io/">Helios</a>, is open source.

I don’t know who’s going to get there first. It could be a framework we haven’t heard of yet. But I do think it will come from a company that understands mobile app development and has experience supporting native app developers.

(Apple? I doubt Apple’s interested. In my dream world Apple designs the services and APIs and gets another company to run it. But Apple, understandably, has zero apparent interest in doing anything that would make it easier to create services for Android, Windows Mobile, and web apps. It’s easy to understand why — it doesn’t sell Apple hardware.)

But — and here’s the important point — we app developers can’t wait. Though I think we’ll have this eventually, it will arrive incrementally, and we need to use what exists today.

<i>Update 12:50 pm</i>: People on Twitter reminded me of another one: [Objective-Cloud](http://objective-cloud.com/).
