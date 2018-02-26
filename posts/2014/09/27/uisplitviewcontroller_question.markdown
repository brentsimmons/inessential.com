@title UISplitViewController Question
@pubDate 2014-09-27 11:55:12 -0700
@modDate 2014-09-27 14:38:12 -0700
Picture an app with three levels of hierarchy. Let’s pretend it’s an RSS reader (it’s not).

Feeds > Timeline > Article

The modern way to make this work for iPad and iPhone is to use a UISplitViewController.

* Left: navigation controller with Feeds and Timeline.

* Right: navigation controller with Article.

Launch in portrait on iPhone 6 Plus. The Feeds view controller takes up the full screen. Good.

Tap a feed. The Timeline appears full screen. Good.

Now rotate — the split view now appears. On the left is Feeds; on the right is Timeline. *Not* good.

And, if I tap a feed, a second Timeline appears in the left, which means *two* timelines are showing.

I have my project set up almost exactly like the Xcode template for a split view controller app. The difference is really just that the master has Feeds and Timeline view controllers, instead of just a single Feeds view controller.

How do I get the Timeline to move to the master (leftmost) side when going from compact to regular horizontal size class?

My question is much like this <a href="http://stackoverflow.com/questions/26060915/having-a-uinavigationcontroller-in-the-master-view-of-a-uisplitviewcontroller-in">unanswered question on Stack Overflow</a>. A difference is that I’m using a selection segue instead of pushing a view controller. (I’m not sure the difference matters. At any rate, we have the same issue.)

<i>Update 2:30 pm</i>: I ran into serious trouble when *nothing I tried seemed to do anything*. Clean builds didn’t help. It wasn’t till I noticed that breakpoints in delegate methods weren’t getting hit — and I was about to file a Radar — that I realized I probably needed to delete the DerivedData folder. So I did, and things started working. So: consider that a reminder.

<a href="https://gist.github.com/anonymous/797aa235dffcf9ed15e3">I’ve published a gist</a> that shows what I’ve got so far. I’m sure it’s not the final version of the code — <code>splitViewController:&#8203;collapseSecondary&#8203;ViewController:&#8203;ontoPrimary&#8203;ViewController:</code> will need more logic — but it solves the problem so far.

Thanks to <a href="https://twitter.com/lithium3141">Tim Ekl</a> and <a href="https://twitter.com/saniul">Saniul Ahmed</a> for help via Twitter.

And — bonus — <a href="https://twitter.com/FriedLemur/status/515974307483512832">@FriedLemur has the tip of the day</a> (regarding DerivedData):

>Option key turns Clean into Clean Build Folder, pretty much rm -rf

That’s *so* much better than me trying to remember where the DerivedData folder actually is.
