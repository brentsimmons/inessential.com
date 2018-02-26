@title Finger is Recordable
@pubDate 2014-03-17 14:30:58 -0700
@modDate 2014-03-17 21:12:13 -0700
[Peter Lewis’s Finger](ftp://ftp.cac.psu.edu/pub/mac/comm/finger/Finger1.5.html) was not just scriptable via AppleScript, it was *recordable*.

If you’re relatively new to the Mac, you may have no idea what that means. The idea is simple: open the AppleScript Editor app (in /Applications/Utilities) and click the Record button. Then go do some things in another app interactively. What you do will be recorded as a script — *if* the app is recordable.

It’s rare that you’d want to keep the script as-is — usually you’d want to generalize it some. But it’s a great way to get started on a script.

I remember this being an important thing for app implementors to do in the ’90s, but I rarely see it mentioned now. (My old apps NetNewsWire and MarsEdit were both scriptable, but neither were recordable.)

A quick tour tells me that some apps are still recordable. Well, the Finder and BBEdit, at least.

[How it works under the hood](https://developer.apple.com/library/mac/documentation/applescript/conceptual/applescriptx/concepts/scriptable_apps.html):

>A recordable application is one that sends Apple events to itself when a user performs actions with the application. If the user has turned on recording in the Script Editor application (with Script > Record), actions that generate Apple events are recorded into an AppleScript script.

I feel certain you could do this with AppKit — but it would be somewhat of a pain. (It was a pain with the Mac Toolbox, too, but since you were on your own to define how your app handled user events, you might as well have picked Apple events.)

At any rate: recordable apps are cool, and I’d love to see the feature get more support from AppKit. But it’s one of those things that’s cool but is perpetually just under the priority horizon. Which I understand.

PS Finger may be old, but Stairways Software is [still making cool apps](http://www.stairways.com/main/).
