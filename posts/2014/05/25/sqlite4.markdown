@title SQLite4
@pubDate 2014-05-25 11:02:59 -0700
@modDate 2014-05-25 11:02:59 -0700
[The Design Of SQLite4](http://sqlite.org/src4/doc/trunk/www/design.wiki):

>SQLite4 is an alternative, not a replacement, for SQLite3. SQLite3 is not going away. SQLite3 and SQLite4 will be supported in parallel. The SQLite3 legacy will not be abandoned. SQLite3 will continue to be maintained and improved.

My software runs on SQLite. I’m happy to see that there will be a SQLite4, and I’m happy to see that SQLite3, which I currently use, will continue to be improved.

One of the changes I like is that the primary key is the <em>real</em> primary key. In SQLite3 the rowid was the key into the storage engine, while in SQLite4 the primary key will be the key — tables won’t even have a rowid, except in the case where no primary key was specified. This should be a performance gain.
