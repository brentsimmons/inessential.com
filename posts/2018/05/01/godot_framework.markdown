@title Godot.framework
@pubDate 2018-05-01 11:08:34 -0700
@modDate 2018-05-01 11:08:34 -0700
I wouldn’t wait for [“Marzipan” or XKit or whatever it is](https://daringfireball.net/2018/04/scuttlebutt_regarding_ui_project).

We don’t know what it is. But my guess — based on my 38 years of writing code for Apple computers — is that it’s something you can use along with UIKit and AppKit, and not a wholesale replacement.

Maybe it’s a declarative API that helps make some things easier, and maybe you can make a cross-platform button more easily. Maybe your table view code could be the same on iOS and macOS. Great!

But don’t expect Macs to turn into large iPads all of a sudden. Macs are gonna Mac. Apps are going to have multiple resizable windows and a menubar. Targets will still be sized and designed for mice and trackpads.

In other words, if you want to write a Mac app, you’re still going to have to deal with the things that are inherently different about Mac apps, regardless of the specific API.

Let’s say this thing ships in the fall of 2019, over a year from now. If past is a guide, we might imagine it would be fun to play with, but not more useful than, say, the original version of Swift. (Swift didn’t get really good for writing apps until Swift 3.)

So it might be 2020 before it’s something that accelerates Mac development in any real way.

You could write a few Mac apps between now and then.

<p style="text-align:center">* * *</p>

I realize that documentation on writing Mac apps is hard to find these days. Books on the subject are rare, and any book you find may be out of date.

But…

One of the reasons I made [Evergreen open source](https://github.com/brentsimmons/Evergreen) is so that people who want to write a Mac app have some examples.

And I just learned that there’s a big list of [open source Mac apps](https://github.com/serhii-londar/open-source-mac-os-apps). This is _way_ more than than was available when I started writing apps for OS X.

I don’t have time to write a book on Mac app development. I wish I did. I might make the time to do a small article now and then, using Evergreen as example. Maybe.

But it’s not my job (as I have to keep reminding myself). It’s Apple’s job to document and evangelize the Mac platform.

(As an additional part of that, I’d like to see Apple update the Mac App Store, and maybe also deal with some of the issues with sandboxing. It would signal that the company cares about Mac apps. I know it _does_ care, but a more public demonstration would be welcome.)
