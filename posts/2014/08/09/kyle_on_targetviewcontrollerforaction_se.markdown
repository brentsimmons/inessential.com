@title Kyle on targetViewController
@pubDate 2014-08-09 15:00:32 -0700
@modDate 2014-08-09 15:40:10 -0700
Kyle Sluder, <a href="http://optshiftk.com/2014/08/targetviewcontrollerforaction-sender-smarter-than-it-seems/">targetViewController&#8203;ForAction:&#8203;sender: is smarter than it seems</a>:

><code>targetViewController&#8203;ForAction:&#8203;sender:</code> does indeed walk the view controller hierarchy, sending <code>-canPerformAction:&#8203;withSender:</code> on the way. But if a view controller returns YES, it will then determine whether the instance’s method for that selector is an override of a UIViewController implementation for the same selector. If not, it keeps looking up the chain.

That’s kind of weird. But, well, it’s pragmatic, too.
