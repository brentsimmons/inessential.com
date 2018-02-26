@title Paul’s Talk on Core Data
@pubDate 2014-02-14 15:25:42 -0800
@modDate 2014-02-14 16:20:35 -0800
We had 50 people at Xcoders last night to see Paul Goracke talk about Core Data. He did a great job, and people were very eager to learn about this particular topic. By show of hands it appeared the room was full of Core Data users. (Enthusiasts, even.)

(I think it was recorded and will appear on the web eventually. Here are <a href="http://xcoders.s3.amazonaws.com/2014-02-13%20Core%20Data%20Potpourri.pdf">Paul’s slides</a>.)

<p style="text-align:center">* * *</p>

I left the meeting feeling a little spooked. *Not* Paul’s fault — it’s more that I’m eternally on the fence about Core Data.

It’s not just that there are certain things that are less efficient in Core Data (one specific: mark-all-as-read in an RSS reader, which means flipping a boolean in a large number of rows, which ought to be just one SQL call), it’s more that there’s a large-ish layer of code and APIs between my code and the database.

Core Data provides a bunch of seriously nice conveniences. I especially like how relationships are handled, which is a pain to do by hand. NSFetchedResultsController is very handy. Etc. <em>So much</em> good stuff.

And yet there’s this layer of glass between me and my data.

And maybe I’m just being a punk for being bothered by it.

<p style="text-align:center">* * *</p>

Here’s a thing I’m looking at right now.

Vesper’s notes UITableView — we actually call it a timeline, since notes are organized by sort date — does not need to be populated by VSNote objects.

A VSNote has more than a dozen properties. But the timeline needs only a few of those, and there would be performance and memory-use gains by using a smaller object. I could conceivably create a VSTimelineNote object with just those few properties. (Truncated text, sort date, unique ID, attachment thumbnail.)

Using <a href="https://github.com/ccgus/fmdb">FMDB</a> I’d query the notes table with something like this: `select id, truncatedText, sortDate, attachments from notes where` something. VSTimelineNote and VSNote would come from the <em>same database table</em>.

To get a similar effect in Core Data I could create two entities: VSTimelineNote and VSExtendedNote. VSTimelineNote would have a to-one relationship to VSExtendedNote.

That’s fine. That would work.

But it’s not great.

It means the data isn’t stored using the most natural representation. The data model would be based on the needs of the UI, which is not a good idea. (But note that I mentioned a truncated text property, which is certainly based on the needs of the UI, so it’s not like I’m against that all the time.)

It also means that some accessors would be weird — to get the creation date, for instance, I’d have to type something like `note.extendedNote.creationDate`.

<p style="text-align:center">* * *</p>

There are other possible Core Data solutions to the problem. For instance, I could do a request that returns an array of dictionaries, use `setPropertiesToFetch:`, and create VSTimelineNote objects (non-NSManagedObject-objects) from that array.

I don’t like that because it essentially means I’m using Core Data as a database rather than as object persistence layer. If I’m doing that, why not just skip the Core Data layer?

<p style="text-align:center">* * *</p>

My listing these options has a point. It’s not to show that Core Data is unflexible or lacks power — it <em>is</em> flexible and powerful.

And it’s not to prove that abstractions are leaky. (Though one-entity/one-table is an obvious example.)

Rather, it’s to show what must be considered a flaw in my developer’s psychology: that I *know* there’s a SQLite database under the hood, and when I think about the Core Data options I can’t help but think how it’s such an easy and straightforward problem to solve were my code closer to the database.

I do *not* recommend that other people adopt this flaw.

<i>Update 4:15 pm</i>: A few people have suggested Core Data’s parent/child entities as a solution to this problem. That might be the way to go. But my point is not that there isn’t a solution, it’s that all of the solutions are a layer on top of what is an extremely simple problem in SQL. (Which is not fair, because Core Data does so much more than just create SQL queries. Nevertheless, it’s hard for me to look past that. That’s my flaw.)
