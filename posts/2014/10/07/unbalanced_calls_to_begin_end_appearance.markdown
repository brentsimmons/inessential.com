@title Unbalanced calls to begin/end appearance transitions
@pubDate 2014-10-07 21:30:11 -0700
@modDate 2014-10-07 21:33:00 -0700
You can <a href="http://ranchero.com/downloads/PopoverRotation.zip">download the test case</a>.

<a href="rdar://18578859">rdar://18578859</a>

Launch using the iPhone 6+ simulator.

Rotate to landscape.

Tap the Show Popover button.

Rotate to portrait.

Note the message in the console, which will be something like: “Unbalanced calls to begin/end appearance transitions for &lt;UITableViewController: 0x7fbb02346170&gt;.”

As bugs go, a message isn’t a serious thing. But it could be indicative of a more serious bug, and so it’s worth reporting.

<p style="text-align:center">* * *</p>

There’s very little code in the test case. The action is in TableViewController.m, which presents a view controller as a popover with an adaptive presentation style (full-screen).
