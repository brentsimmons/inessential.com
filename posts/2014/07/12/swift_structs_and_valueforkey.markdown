@title Swift Structs and valueForKey
@pubDate 2014-07-12 11:57:06 -0700
@modDate 2014-07-12 12:06:10 -0700
Though I’m not writing very much code in Swift, I’m writing a little — and my brain is running a background thread where it keeps thinking about Swift and how my designs will change with Swift.

One of the things that intrigues me is the idea that structs can be used in place of objects in some contexts. Structs make multi-threaded programming simpler, since they’re passed by value and tend to be immutable.

I came up with a good use case, but then I hit a snag.

#### API Code

When Vesper’s sync system gets a JSON reply from the server, it has to turn that JSON into an array of something usable, and then merge those something-usables with existing model objects (NSManagedObject-like objects), and create new model objects when there isn’t an existing object.

The something-usables could be structs instead of objects. They can be created in a background queue (so that the JSON-to-struct conversion happens off the main thread), and then passed to the main queue where they’re merged with existing model objects.

That they’re immutable is perfect. The structs don’t need to change — they’re just a representation of what the server provides. Only the model objects need to change.

#### The Snag

For every merge-able property there are really two properties, and there’s a simple naming convention.

For example, a note’s archived flag has two properties: `archived` and `archivedModificationDate`.

Merging works like this pseudo-code:

<code>if existingObject.archivedModificationDate &lt; serverObject.archivedModificationDate {</code><br />
&nbsp;&nbsp;<code>existingObject.archived = serverObject.archived</code><br />
&nbsp;&nbsp;<code>existingObject.archivedModificationDate = serverObject.archivedModificationDate</code><br />
<code>}</code>

But the code doesn’t actually look like that. Instead of duplicating the above for each property, there’s a single method that takes server object, existing object, and property name as parameters. Then it uses `valueForKey:` on both server object and existing object. (It gets the key for the date value by adding "ModificationDate" to the property name.)

This turns merging a given property into a one-liner:

<code>mergeProperty(existingObject, serverObject, "archived")</code>

(At this point I could, but haven’t, specify an array of property-names-to-merge in a plist rather than in code. I’m partial to that kind of thing, since it allows me to write highly generic and reusable code.)

#### The snag: structs don’t respond to valueForKey

I fired up a new playground and create a simple struct. It worked fine — I could access values via dot notation.

Then I tried `valueForKey` — which didn’t work, as expected.

Because I’d written a bunch of JavaScript code lately, I also tried the following:

`x["propertyName"]`

And:

`x.["propertyName"]`

Neither of those worked, either — but how cool would that have been? And Swift-like, I think, to provide a syntax for KVC rather than force the use of `valueForKey:`.

Perhaps there *is* a way to do this right now, and I just don’t know about it. Totally possible. (<a href="https://twitter.com/brentsimmons">Let me know on Twitter</a> if that’s the case.)

If there’s not, then I can’t use structs in this case, no matter how much it makes sense.

And this is a case where Objective-C’s magnificent suppleness — which we app developers rely on, which we prize — should provide some direction for the future of Swift.

<a href="rdar://17652770">rdar://17652770</a>
