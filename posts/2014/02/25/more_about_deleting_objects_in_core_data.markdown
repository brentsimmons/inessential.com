@title More About Deleting Objects in Core Data
@pubDate 2014-02-25 13:28:04 -0800
@modDate 2014-02-25 13:28:04 -0800
<a href="http://www.cimgf.com/2014/02/25/deleting-objects-in-core-data/">Marcus Zarra</a>:

>Watch for notifications on objects that can be deleted under you. React to those notifications. Plan for them. Presenting an edit view and the object is deleted? React!

The one tricky case in Vesper I have to deal with is, <a href="http://inessential.com/2014/02/22/core_data_and_deleting_objects">as I wrote about</a>, the case where the sync server tells the app that a note has been deleted — while that note is displayed in the detail view.

But, as Marcus points out, this is fairly easily dealt with. I’ll send a custom notification when that note is about to be deleted. The detail view will watch for that notification and do the right thing (which includes dropping its reference to that note). Then the note will be deleted.

So: not tricky at all.

(The only other issue is the timeline, but NSFetchedResultsController — again, as Marcus points out — deals with that quite nicely.)
