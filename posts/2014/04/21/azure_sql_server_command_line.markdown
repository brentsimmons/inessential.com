@title Azure SQL Server Command Line
@pubDate 2014-04-21 11:17:34 -0700
@modDate 2014-04-21 11:21:16 -0700
Database stuff is easy using Mobile Services — it’s a piece of cake to do almost everything you need via the browser or via the [Azure command line](http://azure.microsoft.com/en-us/documentation/articles/xplat-cli/).

*Almost* everything. It’s great until you hit the things that aren’t supported. Then, well, then there’s this weird browser-based SQL Server portal you could use.

But that’s not true anymore. Now there’s [sql-cli](https://www.npmjs.org/package/sql-cli), a Node module that provides a command-line interface to SQL Server. It’s so much like using the sqlite3 command-line interface that I’m at home right away. (It’s written by [Hasan Khan](https://twitter.com/hasank), who’s been a huge help. Just about daily, lately.)
