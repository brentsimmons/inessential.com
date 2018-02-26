@title Correcting the Dots
@pubDate Mon Jun 11 17:29:41 -0700 2012
@modDate Mon Jun 11 17:35:20 -0700 2012
One of the cool things about Objective-C is all the common conventions. My code should look like your code.

But there seems to be one area where we’ve decided that anarchy is okay.

I’m a wild fan of chaos and things-on-fire — everywhere except for code. So here are my two pleas:

1. Use dot notation for properties.

2. Do not use dot notation for non-properties.

Yes, I know it doesn’t matter to the compiled code, but I like having the conceptual difference, and the syntax reinforces that difference.

And while you might not like dot notation — or you might love it and want to use it for things like <code>count</code> that are not properties — I ask you to remember that cool thing about Cocoa where we care about readability and common conventions.

#### Searching

In case the appeal to principle didn’t do the trick for you, here’s a practical case.

Say I’m searching a .m file to find out where a <code>UIImageView</code> gets its image set. Knowing that <code>image</code> is a property, I search on <code>.image =</code> to find out where it gets set.

If I find nothing I start to freak out because it doesn’t make any sense. I check the xib file to re-confirm that there’s no image specified there. I make sure the image view isn’t a public property — it isn’t referenced somewhere else. I even search the project for <code>valueForKey:@"imageView"</code> to see if some other class has cheated to get a reference to the image view. But no.

I know that image view displays an image, and I know the image is set somewhere in that file — and I can’t figure out <em>where</em>.

And then, after wasting time and brain cells, I remember to search on <code>setImage:</code>. There it is.

The above has happened to me. So has the problem of searching for <code>count]</code> in order to find when an array was counted — and not finding it, and getting frustrated, until I remember to search for <code>.count</code>.

What’s the obvious thing to do, the easiest way to agree? Just do what the headers say. If it’s a property, treat it as such. If it’s not, don’t.

And when in doubt, look it up. (If you’re not willing to take a little extra time to do things correctly, then you should probably find another career.)
