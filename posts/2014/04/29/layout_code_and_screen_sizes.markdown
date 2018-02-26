@title Layout Code and Screen Sizes
@pubDate 2014-04-29 18:21:02 -0700
@modDate 2014-04-29 19:16:07 -0700
[Damon Stephenson writes](https://twitter.com/xixora/status/461217971206385665), on Twitter:

>@inessential I personally think that iOS 7 was a trojan horse for wider spread Auto Layout use if they change the resolution in future.

Here’s the thing. Auto layout is absolutely not needed in order to support different screen sizes and resolutions.

Remember the Mac.

We’ve been using autoresizing masks and old-fashioned layout code for years, and Macs have to deal with dynamic layout in ways that iOS apps don’t have to.

Windows can change size. Splitviews can change widths. There are more variations of screen size — and even multiple monitors.

The point of auto layout isn’t to make supporting different-sized devices possible, it’s to make it <em>easier</em>.

I don’t think it’s actually making it easier yet, not when you factor in the learning curve. I think we need better documentation and examples and better tools for debugging. Once we get there — then, yes, auto layout *will* make it easier. But it was never actually necessary for that particular job.

<i>Update 7:15 pm</i>: A case can be made that auto layout is needed for non-integral resolutions: 1.5x, for instance. But I think the chances of seeing this, even on a Mac, are slim. It appears to be a lesson learned. (I could always be wrong, however.)
