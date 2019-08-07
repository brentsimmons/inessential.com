@title Toolbars Without Button Titles
@pubDate 2019-05-23 13:23:48 -0700
@modDate 2019-05-23 14:18:30 -0700
Michael Tsai, in [Mac Toolbar Labels and Accessibility](https://mjtsai.com/blog/2019/05/22/mac-toolbar-labels-and-accessibility/), mentions that he considers showing buttons *and* button titles, at least as an option, preferable to icon-only.

Two things to know about this:

* VoiceOver can still read the button titles
* The buttons display tooltips on mouseover

In other words, it’s still possible to read the titles, and it’s still accessible in at least one important way. However, the titles are not as easily discoverable, and it’s difficult for people who have trouble picking out shapes or associating them with meanings.

Here’s the thing: title-less windows don’t give us the option of showing button titles. No window title, no button titles. I assume most developers would like to be able to offer the option of showing button titles — but they can’t if they also want to use a title-less window. (This is an AppKit thing.)

Title-less windows often make sense for non-document-based apps. Michael mentions MarsEdit, OmniFocus, and ReadKit — and he could have mentioned NetNewsWire too, which uses this style.

<p style="text-align:center">* * *</p>

There’s a hugely important aspect to this: developers follow Apple’s lead when it comes to app design. I’m trying to find Apple apps that allow for buttons *and* titles, and all I’ve found so far is Mail and the iWork apps. (The iWork apps are document-based, which means their windows need titles.)

Some Apple apps with unlabeled buttons include Safari, Calendar, Dictionary, Font Book, iTunes, Xcode, Maps, News, Notes, System Preferences, and Photos.

This is how the platform rolls these days.

<p style="text-align:center">* * *</p>

In fact, lots of Apple apps — and third-party apps — don’t even have configurable toolbars at all. This is a shame. At least with Safari — and the apps Michael mentions, and NetNewsWire — you can rearrange items to your liking, and choose the items you want to see.

Because toolbar customization is part of AppKit, it requires less code than writing your own fixed toolbar. And it’s an easy customization win for your users.

If your designer doesn’t like it, then tell them they need to understand Macs and Mac users better.

<p style="text-align:center">* * *</p>

I’d bet that Mail in the next MacOS release will have unlabeled toolbar buttons.
