@title Vesper Sync Diary #5 - Sync Tokens and Efficiency
@pubDate 2013-11-12 11:24:55 -0800
@modDate 2013-11-12 11:29:59 -0800
Picture this simple web services API as a function:

<code>NSArray \*uploadDeleted&shy;Objects&shy;(NSArray \*uniqueIDs)</code>

(The reality is more complicated, but only barely.)

The client sends an array of uniqueIDs of objects that have been deleted on the client, and the server returns an array of uniqueIDs for deletions that the client may not know about. (Those deletions may have happened on other devices.)

There are two keys to making this efficient.

The first and obvious part is this: the client should send a given uniqueID only once to the server. This is pretty easy to keep track of — if the server responds with 200 OK, then delete that uniqueID locally and never send it again.

The second part is that the server should not send back *everything* — it should send only what the client doesn’t know about. Here’s how I’m handling that.

#### Sync tokens

I’ll explain this backwards, because it makes more sense that way.

When the server responds with an array of uniqueIDs, it also returns a sync token in the response headers. That sync token is an opaque string. The client stores it (but doesn’t understand it), and passes it back to the server on the next call to that API.

On the next call to that API, the server looks for a sync token in the request headers. If it’s there, it cracks it open and finds a date. (The server understands sync tokens, obviously.) It then fetches uniqueIDs *only* since that date. (The date is the date that uniqueID was stored on the server and not the date the deletion happened on the client.)

The server then creates a new sync token and passes it, along with the uniqueIDs it fetched, back to the client. And the client stores that new sync token. The server never has to store sync tokens — it just has to be able to decode them.

(I didn’t invent this, by the way. It was a part of the NewsGator RSS sync API and a part of the Glassboard API. I wouldn’t be surprised to find that this idea is widely used.)

#### Why not just ask for changes since a certain date?

A sync token in Vesper is formed like this:

`1:timestamp` base64-encoded. Like this: `MToxMzg0MjgxNTc2MzU1`, which decodes to `1:1384281576355`.

The 1 signifies that it’s a version one sync token. There could be other versions later — it might be useful to store other data in a sync token.

But I could have avoided all this just by making the API look like this:

<code>NSArray \*uploadDeleted&shy;Objects&shy;(NSArray \*uniqueIDs, NSDate \*sinceDate);</code>

That would have put the responsibility on the client to make syncing efficient — but I think that that’s the server’s job.

It’s the server’s job because I can update the server at any time and make it more efficient. (I could, for instance, add data to the sync token without having to update the clients.)

It’s the server’s job because it’s good engineering to consider the possibility that there could be other clients on other platforms, and we’d be duplicating code if we had to make those clients smart too. Better that the client code is simple and the server code is smart.
