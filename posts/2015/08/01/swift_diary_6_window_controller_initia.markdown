@title Swift Diary #6: Window Controller Initialization
@pubDate 2015-08-01 14:57:21 -0700
@modDate 2015-08-01 14:57:21 -0700
I’m working on UI code — and the below took me a half hour and quite a bit of frustration to figure out, so I thought I’d better write it up.

Here’s the deal: I want my window controllers (and view controllers too) to know about their nib name, but the outside world should not know about their nib name.

Here’s how I handle this in Objective-C: the NSWindowController’s subclass has an init method that references the nib name.

<code>- (instancetype)init {</code><br />
<code>&nbsp;&nbsp;return [self initWithWindowNibName:&#8203;@"SomeNibName"];</code><br />
<code>}</code>

To instantiate the window controller from elsewhere, I just do <code>[SomeWindowController new]</code>. (Could be alloc/init, but I like the fewer characters this way.)

Here’s how to do it in Swift:

<code>convenience init() {</code><br />
<code>&nbsp;&nbsp;self.init(windowNibName: "SomeNibName")</code><br />
<code>}</code><br />

And then I can instantiate the window controller via <code>SomeWindowController()</code>, and all’s well.

Now that I have the answer, it looks so simple. Many Bothans died, etc.

PS Yes, I’m using storyboards, except for the few things that should be nibs.
