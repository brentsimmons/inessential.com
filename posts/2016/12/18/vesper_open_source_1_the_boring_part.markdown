@title Vesper Open Source #1: the Boring Part
@pubDate 2016-12-18 10:33:18 -0800
@modDate 2016-12-18 16:31:15 -0800
I’m making Vesper open source as a historical artifact, because parts of it may be interesting, and not because of any claim that the code is exceptional or that it’s an example of how to write apps these days.

There are good and bad parts of the code. The iOS app, in particular, is definitely old-school — it was written for iOS 6 originally, and doesn’t use Swift, size classes, Auto Layout, and so on. It’s not modern.

Perhaps the main reason for making these open source is that it gives me something to write about.

There are three components: the accounts management site, the API server, and the iOS app. I’ve released the [accounts management site](https://github.com/brentsimmons/vesper-accounts) first.

#### It’s Boring

It’s a Node.js site that ran at https://accounts.vesperapp.co/, which no longer exists. It ran on Azure.

Vesper’s syncing system — see the [Vesper Sync Diary](http://inessential.com/vespersyncdiary) — was home-grown. The biggest reason: the existing systems provided by Apple at the time wouldn’t work for a browser-based app, and a browser-based app was on our to-do list.

We also couldn’t use Twitter or Facebook membership for our accounts system. Partly because not everybody has an account (truly), and partly because we found that people worried that Twitter or Facebook would be able to read their notes. It wasn’t *true* — Twitter or Facebook would have had no access — but we still didn’t want to make people worry.

(Aside: nobody from law enforcement — nobody from anywhere — ever asked us to turn over any data of any kind.)

One of the problems with writing your own sync system with its own accounts system is that you have to provide a website where people can verify their email address, change their password, and so on. That’s what this site was for.

We also used it for internal purposes: so that support could look up individual accounts (though not their notes) and so that we could get stats on current usage.

#### Things I Liked

The best part of this site is that it’s separate from the API server. I like the idea of using multiple sites with a single API server that is the only piece that can talk to the database.

In this case it was just this one additional site, but if we had done Vesper as a web app, it would have been similarly arranged: it would have talked to the API server and *not* had direct access to the database.

Another thing I liked: it’s pretty easy to get things done in Node.js. And Node is a pretty fast server.

#### Things I Didn’t Like

I don’t actually like JavaScript as much as I like Ruby. In retrospect, I’d rather have done this as a Sinatra site. However, the API server was also written in JavaScript, and it was simpler to use just one language for everything server-side.

I had trouble with Jade. Check out the templates in the [views directory](https://github.com/brentsimmons/vesper-accounts/tree/master/views). They look nice and clean, but I found that actually writing HTML this way was a pain. I’d much rather have just written straight HTML.

#### Questionable Decision

The reset-password token was encrypted data rather than a random string. Encrypted in the token was an expiration date (good for two hours), and the app did remember which tokens were used — but only in memory, so it was possible that a token could be re-used if the app was restarted before the two hours was up for a given token.

A better choice would have been to create random tokens and store them in the database — along with username and expiration date — and then delete them from the database when used or expired.

Anybody who got the source code could not have created or decrypted tokens without some additional keys, and those keys were stored outside the repository as environment variables. This is an important concept: source code leaking should be a survivable event. Every component of Vesper was written with that in mind.

#### The One Hard-Coded Secret

Yes, the username for <a href="https://github.com/brentsimmons/vesper-accounts/blob/master/routes/user.js">support’s lookup-user page</a> really was *cano-ichiro*, and the username (though not the password) was hard-coded in the source code.

I leave it as an exercise to the reader to figure out how we ended up with that username. (Hint: to [Dave](http://betterelevation.com/) this username probably made no sense whatsoever.)

#### Thing Not Done

We never had a way for users or even support to delete an account. This was a high priority, but it never got done.

To delete an account I actually went to an Azure-provided database management app and entered in raw SQL to delete an account. This is a *terrible* thing to do. Luckily it was also quite rare. But I absolutely should have made it possible for users to delete their own accounts. (It’s a moot issue now: they’re all gone now.)
