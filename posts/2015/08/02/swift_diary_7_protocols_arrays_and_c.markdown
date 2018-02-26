@title Swift Diary #7: Protocols, Arrays, and Casting
@pubDate 2015-08-02 17:02:12 -0700
@modDate 2015-08-02 17:29:33 -0700
I mentioned before that I’m making heavy use of protocols in my new apps.

Here’s what got me today:

Let’s pretend I’m writing an email client. (This is an example I use on my blog for historical reasons, and should not be taken as indicative.)

I have a tree of Node objects. Each Node has a represented object, which is a data model object. There’s a NodeRepresentedObject protocol.

There are also more-specific protocols. EmailMessage, for instance, is a protocol because I might need different concrete classes for different types of accounts (Gmail, IMAP, POP, etc.).

My class Mailbox has its internal array of email messages. It also has a children variable which is part of the NodeRepresentedObject protocol. Here’s the relevant code:

<code>protocol NodeRepresentedObject : class {</code><br />
<code>&nbsp;&nbsp;var children: [NodeRepresentedObject]? {get}</code><br />
<code>}</code>

<code>protocol EmailMessage : NodeRepresentedObject {</code><br />
<code>&nbsp;&nbsp;// stuff here…</code><br />
<code>}</code>

<code>class Mailbox : NodeRepresentedObject {</code><br />
<code>&nbsp;&nbsp;var messages = \[EmailMessage]()</code><br />
<code>&nbsp;&nbsp;var children: [NodeRepresentedObject]? {</code><br />
<code>&nbsp;&nbsp;&nbsp;&nbsp;get {</code><br />
<code>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return messages</code><br />
<code>&nbsp;&nbsp;&nbsp;&nbsp;}</code><br />
<code>&nbsp;&nbsp;}</code><br />
<code>}</code>

The error is: <code>'EmailMessage' is not identical to 'NodeRepresentedObject'.</code>

That’s true: it’s not. But an EmailMessage *is* a NodeRepresentedObject, so it ought to work just fine.

I tried this:

<code>return messages as [NodeRepresentedObject]</code>

The error: <code>'[EmailMessage]' is not convertible to '[NodeRepresentedObject]'.</code>

Why not? Again — it *is* a NodeRepresentedObject.

The best way I’ve found to deal with this is to map it.

<code>return messages.map { return $0 as NodeRepresentedObject }</code>

That seems crazy. I’m using map to create an array whose members are absolutely identical to the original array. And if it would let me do that, why not allow my original solution? (Or at least the second solution?)

<b>Update 5:30 pm</b>: Filed as [rdar://22109003](rdar://22109003).
