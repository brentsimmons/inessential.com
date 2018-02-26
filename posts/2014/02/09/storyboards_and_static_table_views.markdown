@title Storyboards and Static Table Views
@pubDate 2014-02-09 17:12:43 -0800
@modDate 2014-02-09 17:12:43 -0800
My storyboard has five view controllers that each have a static UITableView and at least one other button.

I really like how easy it is to create static tables and cells using storyboards. Or, I did like it until I learned this: those table views won’t appear unless I also create a UITableViewController for them in IB.

I think this means that I have to embed a container view controller five times and create five separate UITableViewControllers and hook those up. This means my storyboard will have 12 boxes instead of just seven.

Correct? Or is there another way to do this?

The point of the storyboard is, I think, to have a single place to define a bunch of screens that go together, and to get closer to what-you-see-is-what-you-get.

As nice as it is to be able to define static table cells, having to break those off into separate contained UITableViewControllers detracts from the effect a bit.

At this point I realize that all of this would have been easier — for me — in code. But that really just doesn’t seem right.
