@title Singletons follow-up
@pubDate 2014-03-13 16:39:03 -0700
@modDate 2014-03-13 16:48:48 -0700
I figured we were all on the same page about Singletons, but some people have asked me why I used the pattern I used in [my previous post](http://inessential.com/2014/03/13/one_way_to_avoid_singletons).

I should be careful with my terms.

A true singleton is a class where, no matter how many times you alloc/init it, you always get the same instance.

A shared-instance singleton is typically referenced via something like <code>[MyClass sharedInstance]</code>. (Think of NSUserDefaults and NSFileManager.) These aren’t necessarily true singletons, but they might as well be.

A functional singleton is typically created once and then used in multiple places. It’s often passed from object to object — but it’s also often just made a property of the app delegate, and other objects get it from the app delegate.

I don’t like any of these. (Except for the functional singleton that actually does get passed around.)

In our object-oriented happy place, the following is true: an object knows about 1) the objects passed in to it, and 2) the objects it creates and thus owns.

True and shared-instance singletons are created, owned, and retained by themselves. Not happy.

When functional singletons are passed around, that’s good — but when they’re owned by the app delegate, that’s less good, because it means that other objects are reaching across the object graph to get a reference. (And reaching through a UIApplication shared-instance singleton.)

#### The problem of single resources

There is only one application object. An RSS reader has one database of articles. If your app stores pictures as files on disk — for instance — then that folder is a single resource. There’s a single group of settings.

Maybe you’ve got a bunch of these: database, pictures, caches, etc. Let’s call it six things. Are you going to pass all those things around? Rules of good coding say yes.

You might not have to pass all six all the time, but you’ve got to take the time to figure out which ones to pass around, and sometimes you have to be prepared to pass an object through a fairly long chain, through a number of objects that don’t care about it. This makes for more code and more room for error.

So you’ve decided to break, or at least bend, the rules a little bit, because you value simpler code.

The only question, then, is: how are you going to break the rules?

#### How I break the rules

I don’t ever use true and shared-instance singletons. (I did in the past. I stopped.) I don’t like objects that own themselves. Gives me the screaming meemies. I’m ideological on this point, and I realize you may disagree.

I will allow myself a few functional singletons that are owned by the app delegate, because at least they’re owned by *something* — and I’ll even let my objects reach across and grab those. I try to keep this number super-low, definitely in single-digits. (An example is Vesper’s `VSTypographySettings` object, which is used in a bunch of places, and it would be a major pain to pass it through the chain of objects from the app delegate to where it’s needed.)

I don’t like this at all — it feels dirty, for sure — so I keep looking for ways to get this down to zero, but I haven’t made it yet.

In the case I wrote about, `VSRowHeightCache`, I saw no reason to create this in the app delegate, which doesn’t care or know about row heights. It’s used only by the timeline view controller, but its data needs to be shared across timeline instances. (Since it’s common that the same notes appear in multiple timelines.)

So I considered that the actual cached data is another single resource — like a database, the file system, or a group of settings — and that I could allow the view controllers to stay pure by instantiating (and owning and retaining) their own `VSRowHeightCache` instances.

When I realized I could limit the area of the singleness down to an NSMutableDictionary and two C methods, I decided that that was better than a true or shared-instance singleton — because I prefer that to an object that owns itself.

Which, again, you can disagree about — but it allows me to stay in my object-oriented happy place.

The counter argument goes something like this: it really *is* a singleton, no matter how you hide the fact, and the honest thing is to treat it as such. An object is data and behavior, and if the data is singular, then there should be a single object.

Which almost convinces me. *Not* to create it as an actual singleton, but to create it once in the thing that creates timeline view controllers, and then pass that one instance to each view controller. Which I might do.

PS I should, but I won’t, adopt the tag line for this site “[Doing it wrong so you don’t have to](http://kickingbear.com/blog/archives/427).”
