@title Scaling and Performance
@pubDate 2014-04-18 17:52:49 -0700
@modDate 2014-04-18 17:52:49 -0700
In the recent [Accidental Tech Podcast](http://atp.fm/episodes/61) John Siracusa pointed out that I had talked about [scaling](http://inessential.com/2014/03/25/vesper_sync_diary_11_scaling) when I was really talking about performance.

John’s right, and I know better.

In the vernacular sense of *scaling* the two things are related, but I should use more precise language.

So I’ll be more precise: my main goal is to maximize performance and minimize the amount of resources used. My second goal is to design so that I have scaling options if needed.

(Performance is related to scaling only in the sense that it lessens the need to scale, but it doesn’t solve the problem of scaling itself.)

Here’s what I’m doing for actual scaling:

* Using a system that allows for multiple web servers to be automatically created as needed.

* Using a SQL Server database with a maximum of 150 GB.

* Using blob storage for binaries (images), which can scale forever (presumably).

The weakest link here is, I think, the database. If I have to, I can split up the data into separate databases. There are just four tables — accounts, deletednotes, notes, and tags — and each of those could be moved into a separate database. (There are no joins and no foreign key constraints.)

I don’t expect to ever come anywhere near doing that, so I’m not actually planning the migration steps. But it’s in the back of my head that there’s a non-zero probability.

And if I have to go even further, I can. The biggest of the tables, by far, is the notes table. I can break that table out into separate databases, separated by userID. (Which is an integer. Each database would store notes for a range of userIDs.)

And, if that’s not enough, the remaining tables (accounts, deletednotes, and tags) could also be broken out the same way.

I don’t think I’ll ever have to do any of this — but I can, if I need to, with only small code changes.

The web server may also be a weak link. The way to solve this one — not that I think I’ll need to, because I can run a bunch of instances of the server — is to create separate API servers. Each endpoint could be a separate server with its own set of instances. This would require a small code change on the client, but I’d see this coming and make sure it gets done in plenty of time.
