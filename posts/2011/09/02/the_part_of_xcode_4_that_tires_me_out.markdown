@title The part of Xcode 4 that tires me out
@pubDate Fri Sep 02 13:51:34 -0700 2011
@modDate Fri Sep 02 13:57:03 -0700 2011
I use Xcode 4 mostly, but I still use Xcode 3 sometimes for a project that needs it (because it needs the OS X 10.4 SDK).

I started using Xcode 4 in March, and I’ve written a <a href="http://glassboard.com/">brand-new app</a> using it, so I’m not new to it or just now getting used to it.

There are a ton of things I like about Xcode 4. It’s more rational and better-organized in a bunch of ways. The team did a great job thinking things out. There are new features that I appreciate and use. Xcode 4 is a fantastic upgrade.

And yet it makes me feel tired, as if I’m doing the same things over and over. Xcode 3 doesn’t make me feel this way.

I decided to pay attention to this feeling — what makes me feel that way? It turns out it’s pane management.

#### One big window

Xcode 4 uses one big window for the source list, editor, info panes, debugger, text snippets, interface builder, etc. It’s much like Eclipse and Visual Studio in that sense.

I imagine there are two reasons for this (but I’m just speculating):

1. Lots of developers are coming from Eclipse and Visual Studio, and they’ll find this layout more familiar.

2. This saves the developer from the trouble of managing multiple windows.

I can’t argue with the first reason. I could say it doesn’t matter, that the App Store is full of apps even without an Eclipse-like or Visual-Studio-like Xcode, but I don’t know what the Xcode team knows and I don’t know what’s been asked of them.

But I can argue with the second reason. Here’s why: the only thing worse than managing multiple windows is managing multiple panes.

#### Why pane management is worse

The best part about multiple windows is that I can make them any size I want and put them anywhere I want. I can have different windows for different tasks that need different layouts and sizes. A single window with panes doesn’t bring that flexibility.

#### Example: debugging

With Xcode 4 the debugger appears in the main window. When I’m finished I usually (but not always) want it to disappear, so I can get the pixels back for source code editing. Which means I have to hit the hide-the-debugger key command. Again. For the nth time that day (where n is beyond a comfortable number).

Another issue: if the best window size for editing is 1500 pixels wide, but the best window size for running the debugger is 2500 pixels wide (I’m making up these numbers), then I’m in a pickle. Do I resize the main window? Or pick a size that’s less-than-good for at least one of my common tasks?

#### Another example: interface builder

I often like to have the counterpart pane open. But then I open a .xib file — and I can’t see the whole thing because the counterpart pane is open. So now I have to close the counterpart pane, and possibly open the Utilities pane if it was closed before.

How much better if I had a separate window that was already the right size and set-up the way I want it?

#### Wishes

I get it that Xcode 4 probably needs one-big-window as its suggested and primary interface. And I also realize that it’s possible to open multiple windows.

But I do wish I could make it work more like Xcode 3. A separate window for debugging, for build results, for laying-out UI. These tasks are all different enough that using a single window becomes an exercise in pane (I’m tempted to write “pain”) management. And my time and yours is too valuable for that.

And I just don’t want to hit shift-cmd-Y one more time.
