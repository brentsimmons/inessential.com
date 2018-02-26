@title NSSegmentedControl with Menus
@pubDate 2015-03-19 10:53:02 -0700
@modDate 2015-03-19 10:53:02 -0700
Mac developers: you probably recall that you can set a menu for each segment in an NSSegmentedControl, and the menu appears when you click and hold.

The problem with that is discovery — there’s nothing that shows that there’s a menu there.

So here’s what I want to do: put a downward-pointing arrow or chevron graphic to show that there’s a menu. *And* make it so that if you click on the arrow directly, you don’t have to click-and-hold.

But I don’t want to an entirely custom thing: I still want to use NSSegmentedControl.

What’s the best way to do this? Just place arrow buttons on top of the NSSegmentedControl?

I figure I can draw the arrows easily enough by subclassing NSSegmentedCell — have <code>drawSegment:&#8203;inFrame:&#8203;withView:</code> call super and then draw the arrows. But drawing isn’t enough — I want to have an actual button so you don’t have to click-and-hold.

Yet it seems weird to just place buttons on top of a control. How would you do this?
