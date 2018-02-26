@title Paul on UITableViewCell
@pubDate Wed Jan 02 10:30:01 -0800 2013
@modDate Wed Jan 02 10:32:48 -0800 2013
Paul Goracke: <a href="http://corporationunknown.com/blog/2013/01/01/uitableviewcell-is-not-a-controller-but/">UITableViewCell Is Not a Controller, But…</a>:

>I’ve been down a number of UITableViewCell paths that bit me in the end, many of which Brent seems to have experienced as well, but I have ended up settling on creating UITableViewCell subclasses which take the model object they’re intended to display and break out the properties to the individual subviews so the controller doesn’t have to.

Paul makes great points. I’m not persuaded to change my position, but I respect his.

One thing I’ll clarify:

When my view controller is bossing the UITableViewCell around, it’s not directly accessing the cell’s subviews. (Paul assumed it was, which is totally understandable because I didn’t specify.)

I keep a cell’s subviews totally private: they don’t appear in the header file.

Instead, my controller does something like this:

<code>cell.username = username;<br />
cell.statusText = statusText<br />
etc.</code>

In the end, I have a UITableViewCell that knows nothing or almost nothing of the outside world (since it knows nothing of model objects), and that doesn’t expose its implementation (since it doesn’t expose its subviews).

But the most important thing — which Paul and I agree on — is to keep your UITableViewCells stupid and simple. Paul writes:

>Avoid the temptation to bypass the controller and start key-value observing (notifications are also verboten) on the received model object. This is the hubris that will lead to your MVC downfall (been there, done that). Leave all of the updating logic to the “true” view controller, and your cell subclass will remain a happy and healthy data transformer.

If you do use Paul’s approach, there’s one simple piece of advice which should be treated as an absolute iron-clad rule:

>Don’t even keep a reference to the received model object.
