@title On UIKit for Macs
@pubDate 2016-04-01 11:50:54 -0700
@modDate 2016-04-01 11:51:11 -0700
Every time it comes up that <a href="https://medium.com/swlh/macos-it-s-time-to-take-the-next-step-ee7871ccd3c7#.vdfka9e50">Macs should support some sort of extended UIKit</a> rather than AppKit, I think about all the differences between Macs and iOS devices.

On iOS you don’t have to deal with multiple, resizable, movable windows open at the time. Or with being open but not frontmost. Or with a window moving between screens with different resolutions.

You don’t have menus (for the most part), and I’d bet most iOS developers don’t have to think about the responder chain much, or about enabling and disabling user interface items.

There’s no AppleScript support.

And sandboxing is a <em>whole other thing</em> on Macs. Etc.

<p style="text-align:center">* * *</p>

There are plenty the two platforms have in common — and, indeed, we use some of the same frameworks: Foundation and Core Data, for instance. It’s already true that an app can share its under-the-hood code between Mac and iOS. You can even share some UI code via Quartz and Core Animation.

However, there are areas where AppKit and UIKit have the same things but with slightly different APIs: tables, for instance, are similar but different between the two platforms. NSView (Mac) and UIView (iOS) are nearly the same, but aren’t actually the same.

And there are things Macs don’t have at all — navigation controllers, for instance, since they don’t make sense in a context where you can just show the hierarchy via multiple panes.

<p style="text-align:center">* * *</p>

Were Macs to get some form of UIKit, it would have to be extended with all the things Macs need. Let’s assume we’ll still have multiple, resizable, movable windows; we’ll still have a menubar; we’ll still have AppleScript and Services and similar.

Anybody bringing an iOS app to the Mac is going to have to learn those things and handle them. This is a much bigger deal than just getting an iPhone app working on iPads.

I think the premise is that the porting job would be quicker if Macs supported things like UITableView — you wouldn’t have to rewrite your table view to make it work on Macs.

But I have to wonder. Given that there’s a bunch of stuff you’d have to learn and do *in any case*, how onerous is the difference between NSTableView and UITableView? They’re extremely similar already.

Your biggest challenge is probably just that the dimensions of a table view (or most any view) can change arbitrarily, at any time, on a Mac — and you’d have to deal with that whether you were using UIKit or AppKit.

<p style="text-align:center">* * *</p>

I have a theory on why there aren’t more Mac apps.

One is that the additional stuff — menus, live resizing, AppleScript, etc. — is enough of a burden that people just don’t want to do it. You’d still have those things even with UIKit for Macs: they’d have to be added to UIKit, and so that particular burden is not going away.

But I think the more important reason is that Macs aren’t exciting to most developers in the way iOS devices are exciting. Macs are where people quietly get their work done, in much the same ways they did 10 and 20 years ago. There’s your spreadsheet and your word processor. Web browser and email. Graphics editor and text editor. Chat window. You may be swiping a bit these days, but you’re also still just clicking with a mouse.

It’s *boring*.

(That is, until you realize that Mac users love software that helps them get their work done. They support indies and small businesses <em>passionately</em>. Doing great work for these folks is terrifically exciting — but I realize you’re not going to listen to me.)

How do you fix that? How do you make Mac apps exciting to developers?

I think — perhaps surprisingly — that you <em>bring UIKit to the Mac</em>. Even though I’ve spent just about this entire post explaining why it’s not needed and wouldn’t be particularly helpful, I think you do it anyway, as marketing to developers.

There’s a risk, though — once developers realize that UIKit for Macs doesn’t get them out of dealing with all that extra stuff Mac apps need, they may complain that Mac apps are still too much work. Sure.

But I think you do it anyway. Note to Apple: go for it.
