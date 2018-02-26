@title Premature Optimization and Servers
@pubDate 2014-04-15 10:31:40 -0700
@modDate 2014-04-15 10:33:16 -0700
More than one person has suggested I’m guilty of [violating the law](http://c2.com/cgi/wiki?PrematureOptimization) of premature optimization when it comes to my server work.

Here’s the thing, though: when it comes to database schema, I really, really want to get it right *before* shipping.

Making code changes in a client app is normal. Making database schema changes in a client app is a pain, but not the worst thing.

Making code changes on the server is normal too, though a little hairy. But the hairiest of all is database schema changes on the server. I’m designing so that I don’t ever need to do that. (I may not reach that goal. Time will tell.)

Even though Brian Reischl wrote up [how to do data migration](http://inessential.com/2014/04/07/brian_on_data_migration), and so I have a good plan if I ever need to go there, I just don’t ever want to go there.

In other words: getting the server-side database schema right right now isn’t premature — it’s exactly the right time.
