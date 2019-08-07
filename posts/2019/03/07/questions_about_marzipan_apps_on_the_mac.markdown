@title Questions about Marzipan Apps on the Mac
@pubDate 2019-03-07 13:54:36 -0800
@modDate 2019-03-12 11:48:41 -0700
I’m thinking in advance about the things I’d like to know about Marzipan.

My questions, in no particular order:

* Will we be able to ship Marzipan apps that run *only* on the Mac?
* Will we be able to ship Marzipan Mac apps outside of the App Store?
* Will there be a universal app format that includes iOS and Mac versions?
* Will Marzipan Mac apps appear in the Mac App Store?
* Will AppKit be deprecated?
* If AppKit is not deprecated formally, will it get much in the way of new features?
* Will apps have access to AppKit? Can they mix-and-match UIKit and AppKit?
* Will apps be able to support AppleScript?
* Will apps be able to send Apple events to other apps?
* Will we be able to edit the main menu in Interface Builder?
* Will apps support standard Mac customizable toolbars? If so, can these be edited in Interface Builder?
* Will apps have resizable splitviews (without having to write this ourselves)?
* Will apps support fullscreen *with* collapsible/slide-out-y sidebars?
* Will apps support three-paned splitviews (a la Mail) without having to write the whole thing yourself?
* Will document-based apps be able to open a separate window per document?
* Will apps support additional windows? (In Apple News, choose File > Discover Channels & Topics… — what you really want is for that to come up in a separate window, I would think.)
* Will apps support floating windows (such as for an inspector or a social media compose-message window)?
* Will the Macintosh Human Interface Guidelines be updated to account for the differences in Marzipan apps?
* Will table views support drag-and-drop to reorganize without doing the iOS modal thing with the grabbers in the cells?
* Will there be some kind of way to use NSOutlineView (or equivalent)?
* Will table views support standard Mac highlighting? And multiple selection?
* Will sandboxing be *required* for Mac Marzipan apps?
* Will the tab key work to move focus from view to view?
* Will apps be able to use Mac-only frameworks such as SearchKit?
* Is Apple working on a cross-platform, pure Swift app framework that would make Marzipan, UIKit, and AppKit obsolete?

We have hints at some of the answers — see [Steven Troughton-Smith’s blog](https://www.highcaffeinecontent.com/blog/). (Subscribe to his [feed](https://www.highcaffeinecontent.com/blog/rss.xml).) He’s doing excellent work.

But it’s worth remembering that we don’t really know much yet, because even what we’ve learned so far may not reflect the actual shipping reality.

<p style="text-align:center">* * *</p>

I care about the answers as a developer. Though I’m not going to rewrite NetNewsWire as a Marzipan app, I do have a bunch of other app ideas I’d like to do, and many of those should be iOS apps as well as Mac apps.

If Marzipan means I can get those apps made more easily and in less time — *and* that the Mac versions will be as good as an AppKit app, without compromises — then I’ll be happy to adopt it.

But that part is critical. It has to be as good a Mac app as the AppKit version that I would have written. Otherwise it’s not worth my time. Other people may make other calculations, and I respect that.

(Note to those who think of me as a Mac-only programmer: I’ve written several iOS apps, including Vesper, Glassboard, and early versions of NetNewsWire, AllThingsD, and Variety.)
