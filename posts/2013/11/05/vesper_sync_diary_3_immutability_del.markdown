@title Vesper Sync Diary #3 - Immutability, Deleting, and Calculated Properties
@pubDate 2013-11-05 14:38:10 -0800
@modDate 2013-11-05 14:38:10 -0800
[Vesper](http://vesperapp.co/) syncing will work via web services.

I admire the folks who make syncing work via flat files. I assume Omni uses some kind of [Operational Transformation](http://en.wikipedia.org/wiki/Operational_transformation) with [OmniPresence](http://www.omnigroup.com/omnipresence) (though I don’t know this for sure). The folks at Clear [certainly do](http://blog.helftone.com/clear-in-the-icloud/).

But we’re using web services instead. Because:

* I’ve been doing web services programming since the ’90s, since before JSON, REST, SOAP, and even XML-RPC. I’ve been a web services guy for my entire career.

* We don’t want to lock out the possibility of doing a web app, and web apps certainly prefer web services.

* Syncing one user’s data is not necessarily fundamentally different than how my previous app [Glassboard](http://glassboard.com/), a group sharing app, worked. While you might not think to use the word “syncing” with Glassboard, it’s the same thing: it makes your local copy the same as what’s on the other clients, the web app, and the server. It syncs an object graph.

* I’ve done RSS syncing via web services three times. In the process I’ve made a lot of mistakes and learned a ton about syncing.

The above is just to provide background for the things I’m talking about: immutability, deleting objects, and calculated properties.

#### The Black Beast

The worst part of syncing is merging, where you have two sets of data and need to turn them into one. The right one.

When you see duplicate somethings you know that merging went badly somewhere. Or when you know you entered some data and it disappears later.

So one major goal of a sync design is to limit the amount of merging that needs to be done. Here’s how I’m doing that in Vesper.

#### The Data Model

There are just four conceptual entities:

`Tag`<br />
`Note`<br />
`Attachment`<br />
`Attachment Data`

A tag can have many notes; a note can have many tags. A note can have many attachments; an attachment can have just one note. An attachment has one attachment data, and vice versa.

#### AttachmentData is Immutable

AttachmentData has two properties: uniqueID (which matches the uniqueID of an attachment) and binaryData.

Once created, these cannot be changed. This means the app never has to re-download a picture that may have changed. A different picture (or other attachment data) gets a different uniqueID.

(I’ve worked with APIs where the client had to poll a given endpoint to see if a picture had changed. Ugh. Even with [conditional GET](http://fishbowl.pastiche.org/2002/10/21/http_conditional_get_for_rss_hackers/) this is awful.)

#### Attachments are Immutable

While note.attachments — the array of attachments for a note — may change, the individual attachments will not change.

A given attachment has several properties: uniqueID, mimeType, height, and width.

This means that the client can ask the server for attachments created since the last sync and just grab those. It never has to re-download or merge attachments the client already has, and it never has to re-upload an attachment that’s already been uploaded.

Attachment and attachment data may sound like a side issue compared to tags and notes, but in terms of bandwidth they’re just about the entire ballgame. (One picture’s data could be larger than the entire database of notes.)

The simpler attachment syncing is, the more I can be sure that attachment syncing is as efficient as possible.

#### DeletedObjects are Immutable

Okay — there’s one more entity, the DeletedObject.

A DeletedObject has two properties: uniqueID and objectType. The objectType is one of note, tag, or attachment.

One way to support deleting would be to give each entity a deleted property. (Or, in Core Data, probably userDeleted or something that doesn’t conflict with a reserved word.) I chose not to do this, because it means additional mutability for each object type.

Also:

* It implies that an object could be un-deleted.

* It implies that you’d keep the data around for that object rather than really delete it.

I’m doing it like this instead: deleting an object creates a DeletedObject. The original object is removed from the database. The DeletedObject is sent to the server, which then removes its copy of the original object from the database. The next client then downloads that DeletedObject from the server and then removes its copy of the original object.

This makes syncing of deleted objects pretty simple: upload the list of local DeletedObjects since the last sync and download the corresponding list from the server. (Probably in just one call with a return value. Not two calls.) Do the deletions specified by the server.

There is no un-deleting.

Now, I know what you’re thinking. What about undo? What about undoing a delete?

The first thing to remember about undo is that it’s not distributed: it’s a local command, which means it’s implemented entirely in the client. Undo also does not persist after an app has been terminated.

Undoing the deletion of a tag or note is simple: just create a new one, with a new uniqueID, that has the exact same data and relationships as the deleted tag or note. (The client will keep the data it needs to be able to make this work.)

Undoing the deletion of an attachment is also simple: just create a new one just like the deleted version. But undoing the deletion of attachment data requires some special handling, since you don’t want to just give that image data a new uniqueID, which would mean uploading (and downloading on other clients) that data again.

But the answer to that is just code: it just means the client should delay committing the deletion of an attachment until undo is no longer possible. From a UI standpoint you’d never notice, since what governs what you see in the app is the note.attachments relationship, not whether or not the attachment is truly deleted or not.

Attachment deleting can be done extremely lazily, in other words.

#### Not Everything is Immutable

A tag’s name can change in case. (FOO or foo or Foo.) But notes are the main mutable object.

A note can have multiple tags and attachments, and it has the following properties:

`uniqueID`<br />
`text`<br />
`archived`<br />
`creationDate`<br />
`sortDate`<br />
`detectedData`<br />
`attachmentThumbnailUniqueID`<br />
`truncatedText`

That’s a lot of mutable stuff. But, even though a note is mutable, it’s worth trying to limit the number of mutable properties that sync. There are two ways to do this:

1. Find the individual properties that are immutable.

2. Find the properties that can be calculated on the client, that don’t actually need to sync.

Here are the immutable properties of a note:

`uniqueID`<br />
`creationDate`

And here are the properties that can be calculated on the client:

`detectedData`<br />
`attachmentThumbnailUniqueID`<br />
`truncatedText`

This leaves a more manageable set of mutable properties:

`text`<br />
`archived`<br />
`sortDate`<br />
`tags relationship`<br />
`attachments relationship`

That’s not nothing. But it’s also not nearly as complex as the problem seems from a first look at the object graph. It’s not bad — just five things.

Which leaves the question: how am I going to sync and merge those properties?

I’ll answer that in a future post.
