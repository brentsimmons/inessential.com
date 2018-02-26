@title UXKit Skepticism
@pubDate 2015-02-05 14:05:31 -0800
@modDate 2015-02-05 14:09:34 -0800
Some developers are excited to note that the new Photos app contains a <a href="http://sixcolors.com/post/2015/02/new-apple-photos-app-contains-uxkit-framework/">private UXKit framework</a> that, according to Jason Snell, “sits above the Mac’s familiar AppKit frameworks and strongly resembles UIKit on iOS.”

I doubt this will ever be available outside Apple as a framework that’s meant to replace AppKit.

Partly it’s a matter of resources. AppKit exists, and people make great apps with it. It’s hard to imagine Apple wanting to support another UI framework for developers outside Apple.

And it’s hard to imagine Apple adding this complication. Choice of language is one thing — but add the choice of UI framework and it looks like the company is flailing around.

It’s not like AppKit has stood still. With every release of OS X it’s more UIKit-like. It’s not a different country: it has auto layout, storyboards, view-based table views, gesture recognizers, and so on.

But AppKit also has things that don’t make sense on iOS: menus, resizable windows, resizable split views, AppleScript support, drag-and-drop between apps, mouse support, and so on. It has some time-saving (but optional) features such as Cocoa bindings that haven’t made it to iOS.

And UIKit has things that don’t make sense on Macs — navigation controllers and size classes, for instance. And where there are things that are the same on both platforms — toolbars, for instance — you’ll find that they’re not *really* the same.

AppKit and UIKit aren’t that different, and anybody working with one can switch to the other — with a learning curve, sure, but people who stick with one or the other are (hopefully) still always learning anyway.

But where they *are* different, the differences are critical.

With AppKit, Apple does what it does best: steady, incremental improvement. The AppKit of 10.10 is a very nice improvement over that of 10.9, as 10.9 was over 10.8, and so on. I expect that to continue.

#### Minimal UXKit

I could imagine a minimal UXKit that isn’t meant to replace AppKit but that can be used with both AppKit and UIKit. It might have UXColor, which would wrap UIColor and NSColor. Same with UXFont and UXImage. UXTableView could present a simplified superset of UITableView and NSTableView/NSOutlineView. Etc.

The point would be to make cross-platform development a little quicker — but it wouldn’t get you out of using UIKit and AppKit.

And, frankly, a bunch of this is super-easy stuff. You could make your own UXColor class by just defining it to UIColor or NSColor depending on target and adding category methods so that their interfaces match. (<a href="https://github.com/quartermaster/QSKit/blob/master/Classes/QSPlatform.h">I’ve done this</a>. I bet a bunch of people reading this have done it too.)

So I’m not sure there’s that much value in releasing a minimal UXKit — knowing that it would just be a source of feature requests and frustration, because it’s unlikely ever to do enough to make people happy who want to bring their iOS apps to the Mac.

What seems more likely is true convergence: imagine if, in the next OS releases, UIColor and NSColor, UIImage and NSImage, UIFont and NSFont, and so on were actually the same exact things.

#### My own experience

Would UXKit help OmniFocus or Vesper? No.
