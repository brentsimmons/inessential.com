@title Vesper Sync Diary #16 - Debugging Syncing
@pubDate 2014-05-13 11:47:19 -0700
@modDate 2014-05-13 11:51:13 -0700
Some bit of data goes wrong — I do a thing on my day phone, and then check my night phone and it’s wrong.

Were I just debugging the data layer of a single app, I’d have the app running in the simulator and the Xcode debugger, and I’d have its database open in the sqlite3 terminal app, and bugs couldn’t hide for long.

Syncing, at least the way I’m doing it — via web services to a central server — makes debugging more complex. Here’s my setup:

Computer 1 runs Xcode debugger + simulator + sqlite3 for day phone app.

Computer 2 runs Xcode debugger + simulator + sqlite3 for night phone app.

Computer 1 (my main development machine) also has open: Azure portal, [sql-cli](https://www.npmjs.org/package/sql-cli) app (like sqlite3 but for the sync server’s SQL Server database), and the API server code (in [BBEdit](http://www.barebones.com/products/bbedit/)).

Clearly a recipe for fun.

So I do a thing <em>here</em> and see if it ends up correct <em>over there</em>. And, when it doesn’t, I realize that enough state has changed, usually in all parts of the system, that I can’t simply re-run that change. Instead I have to try a similar change.

Where’s the bug? Did the change happen locally as it was supposed to? Was syncing triggered? Did it send the right info to the server? Did the server process it correctly? Did the server store it in the database correctly? Did the other app ask the server for sync changes? Did the server reply correctly? Did the other app handle those changes correctly and update its database? Did it update its UI with those changes?

I don’t have any silver-bullet method for debugging all this. I have all the access and data I need — but every bug is a matter of detective work. A single apparent bug can have multiple causes with fixes needed in the client and server code.

#### Example Bug

Here’s one. The system relies on comparing dates, and I had these two dates:

<code>2014-05-13 04:32:39 +0000</code>

…and…

<code>2014-05-13 04:32:39 +0000</code>

…which turned out not to be equal.

Huh?

Well, <code>timeIntervalSince1970</code> tells me that one date has millisecond precision, and the other doesn’t. The dates really looked like this:

<code>1399955559.325</code>

…and…

<code>1399955559.000</code>

Not equal.

Were this just a single, stand-alone app with no syncing, a bug like this is unlikely: NSDate’s precision would get used everywhere, and that’s that. I wouldn’t even have to think about it.

Where’s the bug?

* The client app might be sending dates without milliseconds to the server.

* The server might be stripping milliseconds in the code.

* The server database might not be storing dates with enough precision.

* The server might be returning dates without milliseconds in its responses.

It could be one or more or all of the above.

The code, on both client and server, is simple and well-factored. For example, there’s exactly one place in the client code where an NSDate is formatted as JSON, and it’s a simple check to see if it’s sending milliseconds or not. So these bugs aren’t necessarily terribly difficult to fix — but it’s still more complex than just doing a stand-alone app.

(Looks like the client code is correct: the format string is <code>yyyy-MM-dd'T'&#8203;HH:mm:ss.SSSZZZZZ</code>.)

Anyway: the good news is that I control all parts of the system. The bad news — the inescapable thing, the thing that makes syncing difficult — is that it’s a distributed system with a bunch of parts.
