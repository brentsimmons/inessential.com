@title 3 laws
@pubDate Wed Dec 23 19:59:53 -0800 2009
@modDate Thu Dec 24 00:14:59 -0800 2009
The Three Laws of iPhone apps:

1. An app must not allocate memory or, through inaction, allow memory to be allocated.

2. An app must obey all didReceiveMemoryWarnings given to it by the system, except where such orders would conflict with the First Law.

3. An app must continue to run and not crash as long as such running does not conflict with the First or Second Law.

Commentary...

\#1 is a bit stringent, but it’s always worth keeping in mind as a paradisiacal condition to strive for, however impossible.

With #2 there shouldn’t be such a conflict, obviously. But possibly worth spelling out anyway.

\#3 seems to be just right.

But #1 is my favorite, the one I keep replaying in my head.

<img src="http://ranchero.com/images/tinyshoe.gif" width="27" height="30" alt="" /><br /><br />

Are there any non-geeks in the audience? If so, allow me to point to the <a href="http://en.wikipedia.org/wiki/Three_Laws_of_Robotics">Three Laws of Robotics</a>.

<img src="http://inessential.com/images/atom.gif" width="29" height="30" alt="" />

<i>Update 12:12 am:</i> I’ve had some questions about this. Obviously, you have to allocate memory. To suggest you shouldn’t is pure hyperbole. My point is just that allocating memory is expensive, and sometimes it can be avoided.

When you run into trouble, use Shark and Instruments to find out what’s going on.
