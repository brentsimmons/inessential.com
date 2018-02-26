@title Brian on Data Migration
@pubDate 2014-04-07 14:06:12 -0700
@modDate 2014-04-07 14:07:30 -0700
<a href="https://twitter.com/brianreischl">Brian Reischl</a>, my former co-worker at Sepia Labs — and cyborg in charge of web services — emailed me after I mentioned that to do a migration I’d “stop the world” first.

(Brian also wrote <a href="http://inessential.com/2013/03/18/brians_stupid_feed_tricks">Stupid Feed Tricks</a>, which, if you’re a fan of the horror genre, is worth reading.)

#### Brian’s Words Are Below

Pretty much any migration can be done without stopping the world. You migrate in steps, with double writes and double reads at some points. Here’s the general outline:

1. Build your new data store. This could be an entirely new technology (NoSQL, different RDBMS), a new server, or even a new table structure in your existing database. 
2. Change your code to write to both the old and the new data store, but continue to read from the old store only. Be sure to capture errors from the new system so that they don’t affect your users, and log them out so you can fix them.
3. Copy your data from the old to new store. But note that the copy process must take into account that some data will have already been written, so it can’t expect an empty store to write to. It also has to account for ongoing changes from your production system. So, for example, if you took a SQL backup of the old store and applied it to your new store, any changes that happened during the backup/restore might be lost. 
4. At this point your old and new stores should be kept in sync automatically. You want to run this way for a while to debug the new store, and ensure that the data stores remain in sync. You may want to run checks to ensure they’re kept in sync. One option is to read from both stores, compare the results and log errors, but then discard results from the new store and only use the results from the old store. 
5. Switch to reading from the new store. You can make the change all at once, or slowly (eg, 25% reads go to new store, 75% old, then 50/50, and so on). Making the change slowly will be more time consuming, but it may reveal any performance or scalability issues before they become a major problem. 
6. Eventually you should be reading only from the new store, and have developed confidence that it’s working properly. Now you can change your code to remove all references to the old store. 
7. Delete the old store. 

Obviously this is far more time consuming than a “stop the world” migration. In return, it gives you a chance to develop confidence in your new system before depending on it fully, and allows you to make the change with zero downtime.
