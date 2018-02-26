@title Development Notes on Glassboard 2.3.3
@pubDate Sat Jan 19 15:22:52 -0800 2013
@modDate Sat Jan 19 16:17:11 -0800 2013
<a href="https://itunes.apple.com/us/app/glassboard/id453661198?mt=8">Glassboard 2.3.3 for iPhone</a> was released on the App Store a few days ago. If you don’t have the update, you should get it.

(If you don’t have the app at all but want to try it out: get it, then open the sidebar, then enter the invitation code <code>rovhy</code> to join the inessential board. And say hi.)

#### Blue Links

The main new feature is that links appear in blue, they’re tappable, and you can have more than one per message. (As in just about every Twitter client ever.)

Though iOS 6 lets you use an <code>NSAttributedString</code> with a <code>UILabel</code> — it lets you create formatted text — it doesn’t give you anything to handle tapping on links. It’s not enough to make them blue. They should highlight on tap and then open a browser screen.

#### Measuring and Rendering Text

To make this work I had to dig into Core Text, which I ended up enjoying. I shouldn’t have put it off so long.

As part of this work I re-did how the message text is measured and rendered. I’m doing measuring and rendering at the same time now rather than as separate steps. I don’t know if this is the best approach or not, but it’s the best approach I’ve found. Here’s how it works:

1. When the app needs to know the height of a cell, it uses Core Text to render the message text. From there it’s simple to find out how tall the rendered text is. That height is cached — and the rendered text itself is cached as an image.

2. When the app needs to draw a cell, it uses the cached image of the text. (The text is actually a <code>UIImageView</code>.)

3. Memory use is considered, of course, and caches can be tossed (in whole or in part) at any time and everything will rebuild when requested.

#### Detecting Links

I also had to find all the links in a message. In my entire career I’ve never shipped software that uses regular expressions. (By design.)

I tried using <code>NSDataDetector</code> to find links, but it wasn’t as liberal as <a href="http://daringfireball.net/2010/07/improved_regex_for_matching_urls">John Gruber’s URL detection regex</a>, so I used that. And thus <code>NSRegularExpression</code> made its first (and so far only) appearance in any of my code.

I felt weird about it. But keyboard and mouse are recovering fine.

(To be clear: I’m using this on plain text, not HTML. Not crossing the streams.)

#### Highlighting Links

It was easy to detect a tap and figure out if the text underneath had a link attribute and then open the browser.

The tricky part was something I hadn’t thought about in advance: you need to *highlight* that link, and the link is not displayed in a single contiguous rectangle. So I had to write code that, given a tap, figures out the array of rectangles in which the link appears.

I did it like this:

1. Get the run of text for the tap location.

2. For that run and all the surrounding runs (before and after), create an array of <code>CGRects</code> (via <code>NSValue</code>). I took the simple approach of looping through lines and runs, and that performed just fine even for text of a few thousand characters.

3. Call <code>setNeedsDisplay</code>.

4. In <code>drawRect</code>, draw a light blue background for the rects for that link.

#### Memory Use Tip

Anyone who’s done this kind of work themselves probably realizes that I’m caching the <code>CTFrameRef</code> in order to handle link tapping. Instruments showed me that this used a surprising amount of memory — so I made the simple change of caching the <code>CTFrameRef</code> *only* when there are links to be handled. For completely plain text there was no need.

#### Design Changes

That was fun. But I spent way more time on design changes.

When I designed Glassboard 2.0, I thought I was exercising a good amount of restraint.

But, really — why did it need wood grain? And curved shadows? And a weird textured navbar? Looking back on it, 2.0 looked more like a crazy baroque craziness than a well-designed app.

I’ve learned alot since then. (And I agree with <a href="http://www.macworld.com/article/2023604/apple-and-the-future-of-design.html">Dave</a> and <a href="http://daringfireball.net/2013/01/the_trend_against_skeuomorphism">John</a> about the future of UI design.)

For the navbar I picked a blue I liked and set the tint color rather than use a custom asset. I like the way it looks, and it gets out of the way. The focus should be on what people are posting, not in things like the navbar.

I spent most of my time on the new timeline. I wouldn’t call it flat — it still has highlight lines and shadows, but it’s much flatter.

My goal was to make it look as if it wasn’t designed at all, as if I just gave up and decided to just put the information on screen in the right order. Or, put another way, my goal was to make it look as if anyone would have designed it that way, as if it was inevitable and obvious.

In my head I kept saying, “Make it look like nothing.”

It would have been easier were the timeline similar to a Twitter app, where everything appears at the same level and with the same weight. But Glassboard shows comments in-line, which meant I had to separate a message/comments group from the next one, and I had to make sure comments appear subordinate.

There are lots of ways to do this — color, indentation, depth, texture — and I spent weeks trying just about everything I could think of. The hard part was to make it not appear visually noisy.

In the end I didn’t go totally flat, and I sweated buckets of pixels over the exact shades of gray and alpha levels for the highlight shadows and so on.

I’ll leave it to you to judge how well I met my goal (or even if the goal was the right goal) — but I will say that I’m proud of the new timeline.

I already see room for improvement, though. As always.

#### Performance and Design Changes

One of the nice side effects of the design change was that I got rid of a bunch of compositing the app used to do. The app used to have that stationary wood background and everything scrolled on top.

Though scrolling was okay, it’s faster in this new version, since I got rid of that effect which wasn’t even awesome in the first place.

#### Lesson Learned

I shouldn’t try to show off. It’s *harder* to just do a good and appropriate job.

Just because I <em>can</em> create a curved shadow and find a wood grain, doesn’t mean I <em>have</em> to use those kinds of things.
