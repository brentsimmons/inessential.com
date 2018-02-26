@title The Bunnies Experiment
@pubDate 2014-03-17 11:08:27 -0700
@modDate 2014-03-17 11:08:27 -0700
After writing about how I was [breaking up Vesper’s timeline view controller class](http://inessential.com/2014/03/16/smaller_please) into smaller objects, I got a bunch of advice suggesting that I go all the way: break out the table view delegates and data source too.

So I decided to try it. I created a basketful of bunny objects.

Here’s the thing: the timeline view controller is complex and the pieces have to work together.

So next I tossed in a ball of yarn to connect the bunnies that need connecting.

The separation into separate objects wasn’t nearly *clean*, in other words. I had to expose a bunch of internal methods and properties of the view controller to its bunnies. Way more than I felt comfortable with. (And there’s no @bunnies keyword to protect those.) 

And some of the bunnies had to know about each other: the drag controller delegate needed to know about the table view delegate and datasource. The timeline cell delegate needed to know about the datasource. Etc.

If I can generalize from this — and I’m not sure I can; it may apply to this case only — I’d say that the more complex a view controller is, the more I want to break it into smaller objects, and the more likely those smaller objects will constitute a *mess*.

#### Happy position

Mess is in the eye of the beholder. I have a low tolerance for a situation where a bunch of objects need to know about each other. (Put another way: I’m happy typing x.y, but too much x.y.z I take as a code smell.)

The key is to find the right balance. Breaking out the animation code (one-third of the timeline view controller) into separate animator objects was absolutely the right thing to do.

Animation code is not like the rest of the code — it’s not like the actions, delegates, and datasource implementations. It’s ugly and specific and it ends up as big blocks of distraction when left in the view controller.

This leaves the timeline view controller at around 2,000 lines, which is way more than I’d like. But I can also say: hey, that’s what it takes to implement the timeline. It’s not extra code. It’s what’s needed, and not more and not less.

#### Warning

Again: I’m not sure it’s right to generalize from my experience with this one view controller. I prefer small, focused objects, and I’m highly sympathetic to the idea that large view controllers should be broken up.

My point isn’t that it’s never a good idea to break up a large view controller. My point is that it’s worth noticing when it’s not actually helping, when it’s adding complexity — and that it’s worth finding the right balance, which takes some thinking. (As for me, for this case, the right balance is to break out the animations and leave the remaining code in place.)
