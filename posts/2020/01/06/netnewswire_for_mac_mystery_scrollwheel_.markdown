@title NetNewsWire for Mac Mystery Scrollwheel Crash
@pubDate 2020-01-06 12:19:54 -0800
@modDate 2020-01-06 14:29:20 -0800
For NetNewsWire for Mac, I get one or two crash logs a week referencing <code>scrollView:&#8203;scrollWheelWithEvent:</code>.

[Here’s the bug for it](https://github.com/Ranchero-Software/NetNewsWire/issues/1513).

Chris Campbell, in a comment, [writes](https://github.com/Ranchero-Software/NetNewsWire/issues/1513#issuecomment-571004938):

>FYI, I see this crash reported very frequently in the commercial Mac app I work on at my Day Job. Unfortunately, we've never been able to reproduce it first-hand. I used a Tech Support Incident to correspond with Apple about this issue (giving them hundreds of sample crash reports), only to have them ultimately give up and credit back the Incident.
> 
> -scrollView:scrollWheelWithEvent: is an API of the private NSScrollingBehavior class and its subclasses (class cluster). Those objects are an implementation detail of NSScrollView that are stored in an external structure, so there is significant opportunity for mismanagement of the memory references.
>
> There has been speculation that "responsive scrolling" is somehow involved…

If you know more about this bug, or have more ideas for working around it, please comment on the issue. Thanks!

*Update 2:20 pm* Jeff Nadeau [writes](https://twitter.com/jnadeau/status/1214310375463669760):

> This should be fixed in 10.15. The 10.15.2 crash I see linked is something different.

This is great news! I hadn’t noticed that almost all of the scrollWheel-related crashes were in 10.14.

I have just one crash log that references the scrollWheel on 10.15, and it includes this:

<code>Assertion failed: (![currentGestureList containsObject:&#8203;self]), function NSScrollingBehavior&#8203;ConcurrentVBL&#8203;AddToCurrent&#8203;GestureList, file /BuildRoot/&#8203;Library/Caches/&#8203;com.apple.xbs/Sources/AppKit/&#8203;AppKit-1894.20.140/Scrolling.subproj/&#8203;NSScrolling&#8203;BehaviorConcurrentVBL.m, line 102.</code>
