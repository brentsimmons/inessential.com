@title UIConundrum
@pubDate 2014-04-25 12:30:03 -0700
@modDate 2014-04-25 12:30:03 -0700
Here’s one.

Storyboard. Static table view, non-scrolling. (It’s beautiful. Everything works.)

Except: I need a button at the bottom of the screen. It can’t be a table footer because it needs to be anchored to the bottom of the screen — 20 pts from the bottom. (No matter what the screen size or table size.)

I thought I could just add it as a subview of the UITableView and give it a couple autolayout constraints.

If I do, I get an error:

<code>Auto Layout still required after executing -layoutSubviews. UITableView's implementation of -layoutSubviews needs to call super.</code>

Well, I shouldn’t be surprised. Adding a subview to a table view willy-nilly is a hack.

But — how do I get that button in there, then?

One option is to use a container view, so that the table view is a subview of the view controller’s view.

But!

If I do that I can’t use that great storyboard feature of laying out static table views, since that works only when the view controller is a UITableViewController, and UITableViewController’s view needs to be a table view. (Correct?)

But I *can* do this, I think, if I use view controller containment. Make the static table view a separate view controller, and have the parent view controller add it. Then I still get storyboards and static table editing.

Okay. That’s one way.

The other option is to use a container view and do the static table view in code. Which means throwing away work I’ve already done and doing things the “hard” way. (Which is not actually all that hard.)

I can’t help but note that if I’d started out in code, I’d be done already, since adding a container view in code is an easy change to make.

So right now I have to evaluate trade-offs:

* Using view controller containment increases the complexity. Another element in the storyboard. Code for embedding the table view controller.

* Doing everything in code means more code. Nice that it’s all together instead of spread out, but it’s still more code.

Also: this applies to not just one but four screens.

Would switching to code allow for a more elegant solution? If I stick with storyboards, is there something else that might come up that would make me wish I had used code?

I don’t know the answers. It’s “maybe” to both.

There’s one thing I’ve learned, though: for me, it’s best to start out with code. I’m most productive that way.

But the question remains of what to do right now in this specific situation.
