@title Swift Diary #3: Arrays, Protocols, and Pointer Equality
@pubDate 2015-07-23 10:10:13 -0700
@modDate 2015-07-23 10:39:25 -0700
Let’s say I’m writing a Finder replacement. (Disclaimer: previous statement may or may not be true.)

The common representation of the file system in a GUI app is a tree. A common pattern, then, is to create a tree data structure. The tree is made of Node classes, and each Node has a representedObject which conforms to the NodeRepresentedObject protocol.

A representedObject may be a Folder or a File. All the Node class knows is that its representedObject conforms to NodeRepresentedObject.

Each Node has zero or more children. The children are Node objects also. The children’s representedObjects are a mix of Folders and Files.

<p style="text-align:center">* * *</p>

Here’s the trouble I ran into. Given a representedObject and an array of Nodes, I wanted to find the Node with that representedObject.

Things to know: the representedObjects are uniqued (a file system folder has one Folder object; a file system file has one File object). And, because they’re uniqued, they’re also objects rather than structs.

Because this is true, I can use pointer equality on representedObjects.

The Objective-C code might look like this:

<code>- (Node \*)existingChild&#8203;WithRepresentedObject:&#8203;(id&lt;NodeRepresentedObject)&#8203;representedObject {</code><br />
<code>&nbsp;&nbsp;for (Node \*oneNode in self.children) {</code><br />
<code>&nbsp;&nbsp;&nbsp;&nbsp;if (oneNode.representedObject == representedObject) {</code><br />
<code>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return oneNode;</code><br />
<code>&nbsp;&nbsp;&nbsp;&nbsp;}</code><br />
<code>&nbsp;&nbsp;}</code><br />
<code>&nbsp;&nbsp;return nil;</code><br />
<code>}</code>

Pretty simple.

<p style="text-align:center">* * *</p>

My first go at doing this in Swift looked like this:

<code>func existingChild&#8203;WithRepresentedObject&#8203;(representedObjectToFind: NodeRepresentedObject) -> Node? {</code><br />
<code>&nbsp;&nbsp;for oneChild in children {</code><br />
<code>&nbsp;&nbsp;&nbsp;&nbsp;if oneChild.representedObject === representedObjectToFind {</code><br />
<code>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return oneChild</code><br />
<code>&nbsp;&nbsp;&nbsp;&nbsp;}</code><br />
<code>&nbsp;&nbsp;}</code><br />
<code>&nbsp;&nbsp;return nil</code><br />
<code>}</code>

This didn’t compile: I get the error <code>error: binary operator '===' cannot be applied to two NodeRepresentedObject operands</code>.

“But,” I thought, ”shouldn’t pointer equality *always* work?”

Well, no. Not if representedObject is a struct.

So it occurred to me that I have to tell Swift that these are both objects, and it works:

<code>if (oneChild.representedObject as! AnyObject) === (representedObjectToFind as! AnyObject)</code>

<p style="text-align:center">* * *</p>

But I don’t like using <code>as!</code> — as <a href="http://martiancraft.com/blog/2015/07/objective-c-swift-core-data/">Rob Rhyne writes</a>, “But every time you type <code>!</code>, someone at Apple deletes a Radar.”

So I figured there must be a better way. And there is.

1. Keep the original line as it was: <code>if oneChild.&#8203;representedObject === representedObjectToFind</code>.

2. Make  NodeRepresentedObject conform to the AnyObject protocol, which lets the compiler know that representedObject is an object, so that pointer equality testing will work:

<code>protocol NodeRepresentedObject: AnyObject {</code>

It works. [See the gist](https://gist.github.com/brentsimmons/71281261478c39adcd3b).

<p style="text-align:center">* * *</p>

Here’s the part I don’t totally like: to make this work, it required bringing in Objective-C. AnyObject is an @objc protocol.

So here’s my question: is there a way to do this without bringing in Objective-C?

(I feel like there are two Swifts. Swift + Objective-C is like writing Objective-C with a new syntax. Pure Swift is another thing. I’m pragmatic, and I’ll use the former as needed — but I want to learn the pure Swift solutions.)

<p style="text-align:center">* * *</p>

<b>Update 10:15 am</b>: the answer came quite quickly from <a href="https://twitter.com/_mattrubin/status/624266521896992768">Matt Rubin on Twitter</a> and others:

>try: protocol NodeRepresentedObject: class { … }

Done! It works.

<p style="text-align:center">* * *</p>

<b>Update 10:40 am</b>: and there’s also this, which I didn’t know, from [Joe Groff on Twitter](https://twitter.com/jckarter/status/624270700614942721):

>AnyObject is marked '@objc' for obscure implementation reasons, but it is a native Swift feature.
