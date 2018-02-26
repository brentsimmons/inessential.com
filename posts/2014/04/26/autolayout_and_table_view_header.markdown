@title Autolayout and Table View Header
@pubDate 2014-04-26 14:15:01 -0700
@modDate 2014-04-26 15:43:23 -0700
What’s the best way to handle this situation?

I have a view that contains a 1) UIImageView and 2) UILabel (multi-line).

I set constraints appropriately. I do *not* specify a width or height for the image view or label, because intrinsicContentSize + constraints should combine to do the right things.

I create a UITableViewHeaderFooterView and I add this view to its contentView.

And… it’s all messed up.

It appears that I need to know the height of the view and sets its frame before adding it to the contentView.

How do I found out the best height for my view? Given the width (width of the superview), I need to know the best-fit height for my view.

<i>Update 3:25 pm</i>: I [created a gist](https://gist.github.com/brentsimmons/11332478) that shows my code.

<i>Update 3:40 pm</i>: Here’s what I expected. Create a view with subviews. Set constraints. Height is calculated from constraints. Everything works.

This reminds me of the old 45-minute rule for CSS-based layout. If it takes more than 45 minutes, punt and just use a table. Since it’s been about two hours, I’m overdue.

The old-fashioned way isn’t that hard, after all, especially given that I’ve done it a zillion times. Override layoutSubviews. Override sizeThatFits. Measure the text. Not rocket science. I would have been done two hours ago. (And it would be less code.)

But it still bugs me. I think that’s part of my anxiety with UI programming — I can master it, but then there are new, better ways of doing things, and those take time to master. Sometimes a lot of time. But I’ve got software to ship.

I don’t feel good about punting. But at least I learned some things, which is progress.
