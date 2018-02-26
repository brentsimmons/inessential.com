@title More on UUIDs and Clustered Indexes
@pubDate 2014-04-15 09:47:43 -0700
@modDate 2014-04-15 09:48:25 -0700
My <a href="https://twitter.com/GlennAlanBerry">SQL Server genius</a> pointed me to this article by Kimberly Tripp about the <a href="http://www.sqlskills.com/blogs/kimberly/guids-as-primary-keys-andor-the-clustering-key/">problem with GUIDs as primary and/or clustering key</a>. (GUIDs and UUIDs are the same thing in this context. Microsoft folks often call them GUIDs.)

<a href="http://blogs.msdn.com/b/cbiyikoglu/archive/2012/05/17/id-generation-in-federations-identity-sequences-and-guids-uniqueidentifier.aspx">Another article</a> suggests this isn’t a big deal with Azure SQL because a network write is slower than a page split anyway.

But the advice still seems to be that UUIDs don’t make the best clustering key. You want something narrow to keep down index size.

So I’ve slept on it. Do I still like this layout for the notes table?

id - auto-incrementing integer clustering primary key<br />
noteID - UUID, unique<br />
userID - int<br />

Yes, I like it.
