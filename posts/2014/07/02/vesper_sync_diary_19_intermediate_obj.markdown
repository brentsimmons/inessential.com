@title Vesper Sync Diary #19 - Intermediate Objects
@pubDate 2014-07-02 13:33:12 -0700
@modDate 2014-07-02 16:04:29 -0700
In the shipping version of Vesper, VSNote, VSTag, and VSAttachment objects can convert to JSON directly. When sending objects to the server, it fetches from the database, then gets the JSON representation of each object (as a dictionary) and sends those (as JSON data).

That’s pretty reasonable, I think.

The thing I like less about the shipping version is how it handles JSON responses from the server. It calls merge routines which compare JSON dictionaries to existing objects. When an object is new it creates a new model object based on the dictionary.

I don’t like this because working with JSON dictionaries is a pain, and it was a source of bugs during development. There are three main issues:

* A value might be NSNull</code> rather than the expected string or whatever, and the merge code had to watch out for this.

* A date value is a string, and the merge code had to deal with converting strings to dates.

* The merge routines use dictionary literal syntax, which is an improvement over <code>objectForKey:</code>, but it’s still less clean and harder to read than accessing properties (such as <code>syncNote.text</code>).

So what happened is that the merge code is really doing two things: 1) converting JSON values to expected types and validating values, and 2) doing the actual merging.

The change I’m making right now is to make these two steps more explicit. It comes at a small cost, but not something a user would ever perceive, so it’s fine. (I’m a mad stickler for performance, and Vesper is praised for being fast — it will remain fast.)

I’m introducing three new classes — VSSyncNote, VSSyncTag, and VSSyncAttachment — which all inherit (ugh) from VSSyncObject.

These classes do the following:

* Init themselves with a model object.

* Init themselves with a JSON representation from the server.

* Generate a JSON representation to the send to the server.

These classes watch for NSNull values and turn those to nils. They handle date conversions.

#### On Sending to the Server

Instead of doing a fetch request and turning model objects directly to JSON objects, the conversion will go model object -> VSSyncObject -> JSON. Yes, that’s extra work, but not noticeably extra, and it centralizes all the conversion knowledge in the sync object.

#### On Handing Responses from the Server

The conversion will go from JSON -> VSSyncObject. Then the merge routines will compare model objects to VSSyncObjects, rather than to JSON.

This means that the merge routines will *not* have to worry about NSNull and dates-as-strings — all that work will have been done before the merge happens, in the various sync objects.

#### What I Like About All This

It makes for more testable code. For instance, I can test JSON validation and type conversions without having to run the merge code.

Another thing I like: conversion to/from JSON can happen on a background queue. Right now this is all on the main thread, since the actual model objects, which are main-thread-only, are involved. (So, in the end, it may be that this change makes Vesper feel even faster, since more work is shuffled to the background.)

But the main thing is cleaner code. The merge routines work and I know they work — they have tests, yes — but every time I look at them it’s hard to see the logic past all the JSON-handling and dictionary access. This way the logic will be made  perfectly clear — and, since this is a super-critical part of the app, it should read like a smart kindergardener wrote it. (Which is exactly how I want all my code to look, come to think of it.)
