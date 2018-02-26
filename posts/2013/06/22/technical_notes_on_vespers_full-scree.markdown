@title Technical Notes on Vesper’s Full-Screen Animations
@pubDate Sat Jun 22 16:06:47 -0700 2013
@modDate Sat Jun 22 16:08:27 -0700 2013
If you’ve checked out <a href="http://vesperapp.co/">Vesper</a>, you’ve noticed that the transition from timeline to detail (and back) isn’t a standard navigation controller transition. The detail doesn’t slide in from the right — instead, the detail view reveals itself as the other notes disappear.

(The same is true for detail-to-picture view and back.)

Though I’ve been writing iOS apps since before the App Store opened, I’d never done any animations like this. I had to figure it out.

#### Smokescreen View

Working on Vesper often makes me think of cartoons like Speed Racer that I loved when I was a kid.

(This is seemingly ironic. The <a href="http://www.youtube.com/watch?v=43rxThjYWsE">Mach 5</a> is all about buttons and gimmicks, and Vesper is all about no buttons and no gimmicks. But it’s not really ironic because I want to capture the same feeling of <em>cool</em> that thrilled my 6-year-old self.)

When I started work on the full-screen animations, I started by lifting stuff up on the z axis and swapping in the next view controller’s view midway through the animation. This totally sucked. Completely. Terrible idea. Just the awfulest thing.

Then I remembered that one of the common escape plans in cartoons was the smokescreen. They’re firing sonic ray bazookas at us! Activate the smokescreen!

So I created <code>VSSmokescreenView</code>. That’s the view where the animations take place. It gets placed at the highest point on the z axis, and the actual view controllers get swapped underneath.

I thought I’d invented something new — but I soon learned that everybody else has been doing it this way for years. Which is cool: it suggests that there’s a best practice and I wasn’t doing something weird.

#### Multiple Animation Blocks

A smokescreen view is easy enough to manage if you have one animation block. Add the view, run the animation, and remove the view on completion.

But Vesper’s transition animations have <em>three</em> blocks (in part because one block would have been too complex to manage).

For example, the timeline-to-detail animation has these blocks:

1. Animate the navbar changes.

2. Animate the table view away.

3. Animate the selected note + thumbnail to its detail-view version.

What’s more, these animation blocks could have different durations, and my designers could change those durations at any time without telling me, just by editing a plist. The shortest one could become longest, and so on.

So the problem was this: how does my code know when to <em>remove</em> the smokescreen view? In which of the three animation completion blocks should this happen?

I can think of a few ways to deal with this. None of them are lovely. Here’s the best one I came up with:

#### Reference Counted Smokescreen View

The smokescreen view has just two methods beyond its init method: <code>incrementUseCount</code> and <code>decrementUseCount</code>. And there’s a read-only <code>useCount</code> property.

Before each animation block, the view controller calls <code>incrementUseCount</code>. In the completion handler for each animation block it calls <code>decrementUseCount</code>.

Once <code>useCount</code> returns to 0, then the smokescreen view is removed from the view hierarchy.

This is reasonably elegant, though I wouldn’t mind to learn of a better approach. (<a href="https://twitter.com/brentsimmons">Let me know</a> if you know of one.)

#### Too Much Information

If you’re used to using standard navigation controllers, you’re used to thinking of each view controller as a silo that exposes nothing about its internals.

Full-screen transition animations like this totally screw with that idea. <em>Something</em> has to do the animating, and that thing needs to know about both view controllers, which means those view controllers have to expose some information they wouldn’t normally expose.

The best thing I could think of was to expose what I needed as properties in the various view controllers, and use a comment to explain that they’re there for animation support only.

Sucky? Yeah, sucky. But way better than the alternative, which would have been to explain to my designers that I couldn’t do the animations because I’m too picky about what goes in my header files. (In plainer language: many Bothans died to bring you these animations.)

#### Rect ’Rangling

I’m a text guy. (See my earlier apps <a href="http://netnewswireapp.com/">NetNewsWire</a>, <a href="http://www.red-sweater.com/marsedit/">MarsEdit</a>, and <a href="http://glassboard.com/">Glassboard</a>.) Even simple addition and subtraction hurts my head. Rectangles vex me. (I don’t know logarithms from drumsticks.) (Which is something I intend to fix, by the way.)

But there’s no way out of dealing with geometry when doing these animations. Something at frame x needs to animate to frame y.

The first thing I learned was this: do not write redundant code to make the smokescreen view’s layout match. Instead, rely on <code>UIView</code>’s <code>convertRect</code> methods to convert from rects in a <code>UIView</code> to rects in the smokescreen view.

Even this hurt my head sometimes. But it got better with practice.

#### Simplifying

One thing I kept repeating in the animations was taking a snapshot of the view-to-animate via <code>renderInContext</code>. What I wanted in almost every case was a <code>UIImageView</code> containing an image of the view.

This was an easy category method to write. Or two methods, actually: one to create a <code>UIImage</code> snapshot of the view, and another to create a <code>UIImageView</code> containing a snapshot image of the view.

There was one thing that made this just slightly more complex: sometimes the animation wanted a clear background and sometimes not. So there’s a <code>clearBackground</code> <code>BOOL</code> parameter on my category methods. (If <code>YES</code>, it saves off the <code>backgroundColor</code> and <code>opaque</code> values, sets those to clear, calls <code>renderInContext</code>, then restores those values.)

Once I got around to writing those category methods (which are simple) I was able to delete a bunch of foolishly-repeated code, which made the animation methods smaller and much easier to deal with.

#### Improvements?

It still bugs me how the animation code looks. It’s so awfully specific, and there’s too much of it.

Some of it is surely the nature of the problem. If you want to do something unique, you have to pay the price in code.

But it goes against the grain: I want it to be simpler and more general. I’ll keep at it.
