@title Memory Graph Debugger Tips
@pubDate 2016-09-22 13:38:42 -0700
@modDate 2016-09-22 13:45:42 -0700
I’ve been using Xcode’s new memory graph debugger for just about a day, so I don’t have a ton to share here, but I do have a few things.

* To start, hit the rotated Sleestak-fingers button in the debugger. It’s between the Cyberman button (view debugger) and paper airplane (location simulator). In other words: it’s not in Instruments. It’s in Xcode.

* Turn off zombies. If your scheme has zombies on, you’re going to get a bunch of extra noise. (Tip: keep zombies off in general until you need them.)

* Turn on Malloc Stack Logging in Diagnostics in your scheme. (I think I have it right that this needs to be on in order for the memory graph debugger to show backtraces.)

* Open the right-hand sidebar in Xcode. Clicking on an object shows its class, hierarchy, and backtrace.

* Lines between objects have a label. A line represents a reference. Click on the label to see if the reference is strong or weak or unknown and what the source and destination are.

* Don’t click on anything where the name looks something like <code>MagicOb</code> (something like that). It crashes Xcode for me every time.

* Click on the circle-with-double-arrows to expand a tree. To unexpand, click again in that same spot. (The arrows point inward now instead of outward.) However, there’s a bug where sometimes this disappears. Select something else in the left-hand sidebar and then come back, and the collapse arrows should appear.

* In the left-hand sidebar, look for the purple icon with the ! inside. These indicate possible problems.

* However, most problems aren’t detected. It’s up to you go through and see what’s hanging around that should not be.

I’ve fixed two bugs using the memory graph debugger, and I saved a bunch of time in both occasions. It’s probably worth telling about them as a reminder of the kinds of problems you can run into.

#### Notification block

An NSNotification observer was set up using a block — which is something I myself don’t do, since it litters an init or viewDidLoad with extraneous code and since it’s *dangerous*.

It’s dangerous because, unless you remember to be careful, it can capture a strong reference to self, and then that object is never going to go away. I don’t like APIs that require the developer to remember extra things like this.

And, sure enough, this was one of those cases.

The tipoff was in the memory graph debugger: the reference was labelled as “capture,” which let me know there was a block doing a capture, and it was then pretty quick to find out where.

(See also, from 2015: <a href="http://inessential.com/2015/05/21/how_not_to_crash_3_nsnotification">How Not to Crash #3: NSNotification</a>.)

#### View controller / view retain cycle

There’s a general rule of programming that says objects should know about their children but not about their parents.

However, sometimes a view needs to know about its view controller. This is less than ideal, but sometimes it’s the least-bad option. (Well… I’m skeptical — but it happens, and we ship great apps, so there ya go.)

The related rule of programming says that if a child knows about its parent, it still can’t hold a strong reference to its parent.

That’s what was happening here: a view was retaining its view controller. The simple fix was to make that a weak property.

And, again, the memory graph debugger took me right to this. I could *see* what was happening inside the app in a way I never could before.

It’s marvelous. You should use it.
