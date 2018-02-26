@title Notes on CloudKit
@pubDate 2014-06-08 17:39:28 -0700
@modDate 2014-06-08 17:49:17 -0700
I [just watched](https://developer.apple.com/videos/wwdc/2014/) the introduction and advanced sessions on CloudKit. I’ve recently written my own [backend syncing system](http://inessential.com/vespersyncdiary) using [Azure Mobile Services](http://azure.microsoft.com/en-us/services/mobile-services/), and that’s the perspective I’ll bring to these notes.

(Disclaimer: Mobile Services is sponsoring this site this week. That’s not why I’m writing this, but I should say that up front.)

First off — holy shit.

It’s closer to the metal than, for instance, iCloud Core Data syncing. The backend is not tied to the local database layer. It handles blobs and structured data.

It differentiates between public and private data.

The APIs are a transport mechanism. It uses change tokens for delta updates (what I called [sync tokens](http://inessential.com/2013/11/12/vesper_sync_diary_5_sync_tokens_and_e)). There’s no magic, and error handling is necessary.

Authentication and identity is handled by the system, and privacy is emphasized.

In other words: it’s wonderful.

#### Limits

Could we have used it for Vesper, had it been available a year ago?

Almost. There are three things that would have prevented it, and the first two are huge.

It’s *only* iOS and OS X. I understand that that’s the point, and I don’t say that Apple’s wrong for doing it this way. I get it. But using CloudKit means not being able to do a Vesper web app, and we’re keeping that option open.

The second thing is that there’s no facility for building services on top of these services — there’s no way to run my own code in the cloud. I require that, because there are services I’d like to build. (How cool if it allowed us to run our own Swift code on the server.)

The third thing that would concern me about using it with Vesper is the limits. It’s possible those will change, and it’s possible that more clarification would take away those concerns.

[Here are those limits](https://developer.apple.com/icloud/documentation/cloudkit-storage/). Some of them looks insanely generous — 1PB for assets storage!

But also notice that the data transfer grows just 0.5MB/user for assets, and 5KB/user for database. That’s not actually that much, and I could see going over those limits. And I know from experience that it’s difficult to estimate in advance what the average user’s needs would be.

What happens if we hit those limits? I don’t know. More information would be good. Actual experience by a number of developers who can share their stories and numbers will also be helpful.

I’ll put it this way: even if we could use CloudKit for web apps, and even if we could add our own code, I’d be concerned enough about the limits to want to talk to folks at Apple to get more information. My suspicion is that Vesper would have been fine, but I wouldn’t have allowed optimism, however reasonable, to prevent me from due diligence.

#### Resemblance to Mobile Services

I mentioned that we use Azure Mobile Services in Vesper. This system is similar in a few ways: there’s a framework that lets you upload and fetch and run NSPredicate-based queries; there’s a portal where you can configure a bunch of stuff; and it uses a just-in-time schema for the database.

At first I thought that structured data was stored in a NoSQL database, but instead it appears that it does what Mobile Services does. When the endpoint gets an object with properties, it dynamically updates the SQL database schema to include any previously-unseen properties.

Then, before you deploy, you freeze your schema.

I don’t think that CloudKit is built on Mobile Services, but it’s possible that it’s built on some of the same tech. That just-in-time schema seemed very Azure-like to me. (I know people. Everyone says they can’t confirm or deny, which is not a surprise, but we do believe that [Apple has used Azure](http://daringfireball.net/linked/2014/02/04/icloud-azure) for other iCloud services.)

#### Resemblance to Azure Table Storage

At first I thought that structured data was stored in Azure Table (NoSQL) storage because of the references to zones. A zone in CloudKit could correspond to a table in Azure table storage or a container in Azure blob storage.

And it’s totally possible that structured data actually *is* stored in NoSQL table storage, and it just looks sort of like SQL because it enforces a schema eventually, but I doubt it. 

Unstructured data, however, would have to be stored in Azure blob storage or something like Amazon S3. (It’s entirely possible that Apple uses multiple providers, of course.)

#### Summary

One of the slides said that syncing is hard. While this makes it much easier, it doesn’t do *everything*. You still have to handle errors and conflicts. It takes design and work.

But that’s to be expected.

And it’s nice. Real nice.

Could you write a traditional RSS reader with a content service with it? If you could figure out how to get your feed crawler to get content into the public database. If you can figure out an efficient way to store read/unread states of many thousands of items per user. So: maybe.

How about Glassboard? CloudKit has public and private data, but no groups, so this would take some trickery. If you could do it, it would be at the expense of bending some things, and it might not be secure. And then you’d have to kill the web and Android clients. So: no.

But I still bet that lots of apps will benefit from this. Somewhere people are thinking about their existing apps and how they’d benefit — and people are planning new apps that they wouldn’t have otherwise been willing to try.

I think this is going to be a huge deal. I think it’s the first time Apple has really nailed a web service for developers. And I tip my hat to the team (or teams) behind all this. Good job, folks.
