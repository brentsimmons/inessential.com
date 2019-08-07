@title NetNewsWire Diary #2: Switching to OPML
@pubDate 2018-09-27 13:35:18 -0700
@modDate 2018-09-27 13:35:18 -0700
Since the earliest days of NetNewsWire, before 1.0 even shipped, I wanted to make the subscriptions list on disk an [OPML](http://dev.opml.org/) file.

It seemed like using the standard format for listing RSS subscriptions would be a good idea. But I was never able to make that happen — until now, with [NetNewsWire 5.0d7](https://nnw.ranchero.com/2018/09/27/200359.html).

#### Why It’s a Good Idea

Given that OPML import and export is a must-have feature — which NetNewsWire already has — then storing the subscriptions on disk as OPML means less code, because there’s just one format to support, instead of supporting both OPML and a custom format for just the app.

It means that the OPML reading and writing code will run for every user on every session, which means any bugs in OPML support won’t be able to hide.

It means a user can get their subscriptions list and move it to another system without first having to launch the app and do an export — the OPML file is already there on disk already.

It also means a user could replace their subscriptions list on disk by swapping in a different OPML file, without having to figure out how to do it through the app.

#### Why I Never Did This Before

The problem, though, is that the standard OPML format for listing RSS feeds doesn’t have slots for additional metadata. I want to store things like Conditional GET information, the hash of the contents from the last fetch, the edited name as well as the feed’s declared name, and so on.

So for all these years I thought, “Well, that’s too bad. I wish I could use OPML, but I can’t.”

#### Why I Could Do It Now

It occurred to me I could use a “side table” — that is, a separate place to store feed metadata. This would allow me to store whatever additional data I wanted to store in a separate location.

The go-to for this would normally be SQLite, with some kind of table for feed metadata.

But this has another problem: SQLite is structured storage. There’s a schema. But this doesn’t quite suit feed metadata — especially not when you add in syncing. I wanted the ability to store attributes for each feed without knowing, in advance, what all those attributes might be.

Enter [Rainier](https://github.com/brentsimmons/Rainier), the inspired-by-UserLand-Frontier app I’m working on. It includes an object database — that is, it includes a hierarchical, schema-less, key-value database. It’s like a dictionary that can contain nested dictionaries.

Which is *perfect* for what I wanted to do: I could make each feed a table in an ODB database, and then each feed can store arbitrary key-value pairs. (Think of a “table” in an ODB database as really a dictionary.)

So I built this ODB storage — perhaps ironically, it’s built on top of SQLite, but why not? SQLite is amazing — and its first use is in NetNewsWire.

Rainier-the-app isn’t far enough along to actually do anything at all yet. But a key component of it is now part of NetNewsWire. I expect this pattern to get repeated for a few more things, too — including the (not-nearly-finished) scripting language.
