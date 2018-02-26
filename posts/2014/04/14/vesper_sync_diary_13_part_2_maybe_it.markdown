@title Vesper Sync Diary #13 part 2 - Maybe It’ll Be UUIDs After All
@pubDate 2014-04-14 15:14:25 -0700
@modDate 2014-04-14 15:26:07 -0700
I slept on the thing about <a href="http://inessential.com/2014/04/13/vesper_sync_diary_13_unlucky_13">using 53-bit integers as note IDs</a>. I woke up and it felt weird — slightly but detectably. I listen to those feelings.

As previously mentioned, I’m still learning my new environment. Any new environment takes time. The thing to do, when things seem weird, is more research.

Though the initial problem was a JavaScript problem, the thing I’m trying to optimize is a SQL Server database. So I’m doing some more research on the database.

#### UUID data type

SQL Server has a UNIQUEIDENTIFIER type. (Sorry for the shouting, but database people are shout-y.)

I assume this saves space over just using a 36-character UUID string — I figure it strips the dashes, at least.

That’s wider than a 64-bit integer, and I don’t love it, but it’s not the worst thing ever to happen. The great thing about UUIDs is that they can be created on the client and guaranteed (for practical, real-world values of “guaranteed”) not to collide.

(Remember that, in Vesper’s case, a note ID need be unique only for a given user.)

I *really* wanted 64-bit integers. But I’m willing to accept UUIDs because it’s not weird and is a standard practice.

#### Clustered indexes

Azure SQL Server insists that each table has a clustered index — that is, an index which tells the database how to physically lay out the data.

The primary key is by default the clustered index. The primary key for the notes table is noteID + userID.

Recall that UUIDs look like this:

4C958F48-A332-44D2-A0AD-3E91EF172C6D<br />
0ACA46EE-86F8-4443-BF51-A52A4506FD6C

There’s no order to them. So, to insert a new note could mean inserting it anywhere in the table rather than at the end.

That sucks.

(Yes, I know about NEWSEQUENTIALID(), but I’m generating IDs on the client.)

But here’s the thing: I had this exact same problem <em>even before</em> using UUIDs, because I was using random integers.

What I want instead is a way to add a row at the end, like adding a page to a book. For that I’d need to create a separate identity column with a monotically-increasing integer — like adding a page number — and then make *that* the clustering key. (The primary key and clustering key do *not* have to be the same.)

#### Alternate approach

Having primary key as noteID + userID, and a separate identity clustering key, is just about the same thing as this layout:

Primary key: identity integer (page number style)<br />
Constraint: noteID + userID is unique

This alternate approach feels more right.

My goal is to make noteID + userID unique, and to enable fast lookups. Adding a constraint (which adds an index) makes that work. I don’t also have to make it the primary key.

#### Do I still have the problem of JavaScript and big integers?

Does my code ever need to see the identity integer? The clients don’t — it’s a server-side detail only.

But if my server-side JavaScript code needs to reference it, then once it passes <a href="http://inessential.com/2014/04/13/vesper_sync_diary_13_unlucky_13">9007199254740992 notes</a> then we’re screwed.

You know what? I’m fine with that. To hit that number, every human on Earth would have to create over a million notes. I won’t worry about it. I’d be a billionaire long before then, and my blog posts will be me figuring out which island I should buy.

(With that much money this problem would be solvable, in other words. Solvable by other people who I pay very, very well.)

#### Summary of changes

I think it’s a plan.

Client will have to make these changes:

* Generate note IDs as UUIDs.
* Store note IDs as UUIDs. (Change database schema and data model objects.)
* Fix code that expects note.uniqueID to be a 64-bit integer.

Server will have to make these changes:

* Update notes and deletednotes tables to have an integer identity clustered primary key.
* Update notes and deletednotes tables so that noteID is a UUID.
* Updates notes and deletednotes tables with a unique constraint on noteID + userID.

<em>The good news:</em> it’s possible that none of the server-side JavaScript will have to change. If there are any changes, they’re few and small.

<em>The bad news:</em> there’s more client-side code to change than I’d like. Normally a schema change in a development version isn’t a rough thing, but it does mean going into the database migration code again, which I don’t like doing.

<em>The other good news:</em> but the database migration will actually be simpler, since I was using UUIDs for note IDs in Vesper 1.0. I can preserve those UUIDs across the migration, where until just now I was changing note ID to 64-bit integers. So that’s cool. Simpler data migration is better.

<strong>PS</strong> The only thing that gives me pause — and something <em>always</em> gives me pause — is the idea that I could make userID + noteID the primary clustered key. (userID first.) This would mean that notes don’t get added at the end of the table — but all notes for a given user would be stored together. I think. I don’t have an easy way to test this, but my gut says that adding notes at the end is the better way to do this, and I should just rely on that unique constraint index to make lookups fast.

This is where the value of knowing your environment comes in. If I had five years, say, of SQL Server experience, I’d probably just know the best answer.

Well, the only way to learn an environment is to work in it, and that’s what I’m doing. Later I may look back and laugh. (Wouldn’t be the first time. Not even close.)

<strong>PPS</strong> If it seems like I’m working things out by writing them up here, it’s because I am.

Also, if it seems like I sometimes have to try <em>everything</em> before I get to an answer I like — well, that’s often also true.

<strong>PPPS</strong> Why did 53-bit integers seem weird enough to bug me? I have to plan for all options. There’s always the chance that another developer helps with this code — web app, for instance. Or we could make the API open. (Doubtful, but I have to plan for craziness.) Would the 53-bit limit be observed? It’s a data corruption bug waiting to happen. Even though it’s one little thing — an upper limit on note IDs — it’s too much complexity. Sync needs to be as simple as possible.
