@title A Quick Cheat I’ve Used
@pubDate Mon Dec 31 17:16:28 -0800 2012
@modDate Mon Dec 31 17:16:28 -0800 2012
Given a UITableViewCell, you can get its indexPath and, thus, the model object it represents.

But you can also cheat at it. I’ve done this in the past, and I’m not sure how I feel about it.

<code>#import &lt;objc/runtime.h></code>

The above line should be scary. Just because you can build planets out of proto-matter doesn’t mean that you <em>should</em>.

<code>static const char *BSAssociatedModelObjectKey = "BSAssociatedModelObject";</code>

In your view controller, in <code>tableView:cellForRowAtIndexPath:</code>, after getting the cell and looking up the model object:

<code>objc&#95;setAssociatedObject(cell, BSAssociatedModelObjectKey, modelObject, OBJC&#95;ASSOCIATION&#95;RETAIN);</code>

Then, later, when you have a cell and needs its model object:

<code>modelObject = objc&#95;getAssociatedObject(cell, BSAssociatedModelObjectKey);</code>

This way the model object is associated with the UITableViewCell — but the UITableViewCell itself doesn’t know that or know how to look at it. It’s just a convenience for the view controller.

I’m not sure that the convenience is worth it — it’s not like it’s hard to go from a cell to its model object. And any time you’re getting the runtime involved is weird. Red flags go up — with your name on them, embroidered with radium thread.

But. I can’t help but like it anyway, even though I don’t actually use associated objects in this way. (Anymore.)

If this is all new to you, see Ole Begemann’s <a href="http://oleb.net/blog/2011/05/faking-ivars-in-objc-categories-with-associative-references/">Faking instance variables in Objective-C categories with Associative References</a>.
