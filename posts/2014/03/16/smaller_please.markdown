@title Smaller, please
@pubDate 2014-03-16 15:16:40 -0700
@modDate 2014-03-16 15:16:40 -0700
Vesper’s timeline view controller is a monster class. Xcode tells me it’s 2,950 lines long (including blank lines), which is at least five times larger than I’d like it to be. Ten times larger than ideal.

A third of that code is transition animations.

Since Vesper was written for iOS 6, it was written before the new UIViewController transitions API. It’s time to switch to the new API.

(It’s amazing how an app less than a year old can incur technical debt. One thing I’ve learned is to deal with debt sooner rather than later, before I spend all my time paying interest.)

Here’s the plan:

1. Break the animation code out into separate classes that implement <code>UIViewController&#8203;AnimatedTransitioning</code>.

2. Get that code to work with the existing system. (Without actually using the new transitions API.)

3. Decide whether or not to stop there for the next release.

4. If not stopping there, then modify the current view controller hierarchy so that it’s using a UINavigationController. (Right now it’s not, because a UINavigationController wouldn’t have worked for us in iOS 6.)

I like the plan because I have the option of not going all the way, and I’d still get benefits: partial tech debt reduction and better-factored code.

But that will get the code down to about 2,000 lines. I need to break this up some more.

#### Going Lighter

Chris Eidhof’s [Lighter View Controllers](http://www.objc.io/issue-1/lighter-view-controllers.html) (objc.io #1) has some good advice: separate out data source and other protocols, move domain and web service logic into the model layer, and move view code into the view layer.

In my case, domain and web service logic is already where it belongs, outside the view controller.

What I do have is a bunch of delegate implementations — VSTimelineCellDelegate, UIScrollViewDelegate, UISearchBarDelegate, UITableViewDataSource, UITableViewDelegate, VSTableViewDragControllerDelegate, and UIGestureRecognizerDelegate — some view layout code, and some action methods.

I could move the view layout code to the view easily enough. (About 80 lines to move.) I think I’ll leave the action methods in place, since I consider actions part of the heart of a view controller.

Which leaves all those delegate implementations. While wisdom these days suggests moving UITableViewDataSource and UITableViewDelegate out of the view controller, I’m not sure I agree. I want the view controller to contain its very most core code, and I consider that core code to be UIViewController overrides, actions, touch handling, and table view datasource/delegate. (Reasonable people may disagree.)

Which still leaves a bunch of delegates that could be moved into separate classes: VSTimelineCellDelegate, UIScrollViewDelegate, UISearchBarDelegate, and VSTableViewDragControllerDelegate.

Moving those out probably won’t get the class down to 500 lines, but it’ll be close.

#### The Danger

I’ve gone on ensmallen-all-the-things kicks before, and what sometimes happens is that small objects proliferate like bunnies, and one day I end up looking at it and saying, what *is* all this shit? How can I possibly need 10 different objects to implement one goddamn view controller? How do they all work together?

So, while I *do* have to cut down this big view controller, I have to be mindful that, in a way, I’m just shuffling complexity around rather than reducing it. Smaller, focused objects are better — but there’s still a complexity cost in having more things that work together. And it’s easy for me to go too far in that direction.
