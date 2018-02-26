@title First Go at Using IB_DESIGNABLE and IBInspectable
@pubDate 2014-11-08 17:26:41 -0800
@modDate 2014-11-08 17:29:38 -0800
In AppKit, views don’t have a backgroundColor property. This isn’t a great big pain or anything — just a small thing. But nice to solve.

There are many times when I have a view that contains other views and the container view should have a background color. (And be opaque. I’m a big fan of opaque views.)

And sometimes I just need a divider — and a divider is, after all, just a thin view with a background color.

And I’d really love it if I could set the colors in Interface Builder, and I’d love it if IB actually drew the correct background colors. That would go a surprisingly long way toward making IB a WYSIWYG editor.

So here’s what I did:

Created BackgroundColorView.

In the .h file:

<code>IB_DESIGNABLE</code><br />
<code>@interface BackgroundColorView : NSView</code><br />
<code></code><br />
<code>@property (nonatomic) IBInspectable NSColor *backgroundColor;</code><br />
<code></code><br />
<code>@end</code>

In the .m file:

<code>- (BOOL)isOpaque {</code><br />
<code></code><br />
<code>&nbsp;&nbsp;return YES;</code><br />
<code>}</code><br />
<code></code><br />
<code>- (void)drawRect:(NSRect)r {</code><br />
<code></code><br />
<code>&nbsp;&nbsp;[self.backgroundColor setFill];</code><br />
<code>&nbsp;&nbsp;NSRectFill(r);</code><br />
<code>}</code>

And then in IB I just use a BackgroundColorView (I set the Custom Class to BackgroundColorView), and it does what I want. I can set the color in IB, and IB draws the correct background color.

I like it. It means that I’m not the bottleneck — designers can change the background color themselves. Cool.
