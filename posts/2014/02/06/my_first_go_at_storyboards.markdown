@title My First Go at Storyboards
@pubDate 2014-02-06 20:22:39 -0800
@modDate 2014-02-06 21:33:56 -0800
In one of my projects I have a great case for storyboards: a collection of screens that appear in a navigation controller. Each screen has some buttons plus a UITableView with static cells.

I don’t tend to use Interface Builder very much, and this is my first go with Storyboards.

#### What I Like So Far

- On my big display I can see six screens all at once. (There are seven in this storyboard.)

- Creating static cells is easy.

- Storyboards understand view controllers and have a bunch of configuration options — other xib files don’t. (File’s Owner could be anything.)

#### What I Don’t Understand Yet

I’m still learning. Some things are not obvious yet.

Here’s my case: UIView with embedded UITableView and with other buttons.

How will the UITableView resize? Here are some of the options under View Controller in the inspector:

- Adjust Scroll View Insets

- Resize View From Nib

- Extend Edges Under Top Bars

- Extend Edges Under Bottom Bars

- Extend Edges Under Opaque Bars

I have *no idea* what combination of these will work. And I don’t know how any of these interact with Autolayout.

For instance, “Adjust Scroll View Insets” corresponds to the `automaticallyAdjustsScrollViewInsets` property, “which allows the view controller to adjust its scroll view insets in response to the screen areas consumed by the status bar, navigation bar, and toolbar or tab bar.”

But what if the scroll view is a subview of the top-level view? Will this do what it sounds like, or not?

There’s an answer, but I don’t know it. (I’m not asking what it is — I'll find out.)

#### What Frustrates Me

I can’t make the screens match the design.

There are a half-dozen or so things I want do — create custom header and footer views for table sections, set the color of the navigation bar title, use custom fonts, etc. — that I can’t figure out or are not possible.

This isn’t really a new thing with Interface Builder — we’ve been dealing with this all along — but it’s weirdly <em>more</em> frustrating the closer we get. I want to give this to my designers and let them make it perfect without even having to run the app, but I can’t. Yet.

It’s 2014.

#### What Worries Me

My designers *will* dig into this, and then we’ll have to merge.

#### What Surprises Me

One of my screens is a blank view controller — it’s a container for two other view controllers. (One shows or the other shows.) We have plenty of code support for this kind of thing, but it appears there’s nothing in Interface Builder.

<i>Update a few minutes later:</i> I was wrong — there totally <em>is</em> a thing in Interface Builder for this. You can drop in a container view and set an Embed relationship to other view controllers. This is cool. I like this. (This info comes from [Doug Russell](https://github.com/rustle/accessibility).)

#### What I Think of Autolayout

The improvements to Autolayout in Interface Builder in Xcode 5 are good and quite welcome — but I’m still going to go with Autolayout in code instead.

I tried it in IB, but I found it went like this: select the thing I’m working on. Click on a constraint all the way on the left. Click in the inspector all the way on the right. Click on the layout toolbar. Repeat in random combinations. And then struggle to resolve ambiguities.

It’s a bunch of moving around. Related things aren’t near each other. It doesn’t compare to reading code (even Autolayout code, which can be verbose but is linear and contained).

(I’ll have my designers write Autolayout in ASCII in [DB5](https://github.com/quartermaster/DB5).)

#### What I’m Going to Do

I’m going to keep using Storyboards when I can, when it’s appropriate. The things I like I really, really like. The things I don’t understand I will come to understand.

It’s clear that Storyboards are the future, and only an unwise programmer refuses to keep up.

And the things that frustrate or worry me — well, I expect those to improve over time. (I’ll file radars.)

In the meantime, I can’t help but think how awesome it would be if my designers really *could* build the UI in Interface Builder.
