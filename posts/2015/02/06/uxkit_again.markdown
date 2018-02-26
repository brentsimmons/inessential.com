@title UXKit Again
@pubDate 2015-02-06 13:26:26 -0800
@modDate 2015-02-06 16:41:16 -0800
Garrett Murray, one of the great iOS developers, <a href="https://twitter.com/garrettmurray/status/563791888369467392">tweets</a>:

> I do sort of dream of this world though where building UI for iOS/Mac/Watch all uses very similar code.

You could say that *it already is* very similar code. Everything under the hood is the same — Foundation is the the same, Core Data is the same, networking is the same, and so on.

The code that needs to be different is UI code. But, even there, you have so many things that are again the same (auto layout and storyboards) and things that are very similar, that use the same concepts with slightly different names (colors and fonts, gesture recognizers, view controllers, table views, text views, image views, popovers, and so on).

The big differences — and there are some — can’t be attributed to the frameworks: they’re differences of the platform.

An example: iOS uses navigation controllers for hierarchical data, while Macs use multiple panes. (I’m aware that iOS has split views, but, in general, iOS uses time where Macs use space. I’ve never seen a three-paned iOS app, and I hope I never do.)

Macs have menus and multiple resizable (closable, minimizable) windows. Macs have configurable toolbars; Macs have mice. Macs let you drag-and-drop between apps. Mac apps are scriptable.

By the time you’ve unified all this into one framework, you’ve either done a disservice to one or both platforms (by removing or changing things that people expect from the platform), or you haven’t really gained anything, as the differences between the platforms still need to be expressed in the framework, and learning how to write Mac apps would still be roughly the same-sized job it is right now.

Programmers like it when differences can be collapsed, when we can use one thing to make two things happen. But we also have to remember that different things really should be different — and not just different, but *obviously* different.

I have no illusions that I can talk any iOS developers into Mac development. I will say that it’s *fun*, though, for a bunch of reasons. Your apps run on the same machine as your development environment. You have the freedom to distribute outside the app store. You have a chance to write something that all your peers — many of whom are also programmers — will run all day long on *their* Macs. (And you have a decent chance of <a href="http://www.panic.com/blog/the-2014-panic-report/">making better money</a>. Mac users tend to be loyal and supportive and awesome.)

The thing to do isn’t to treat the Mac as a weird version of iOS, though. The Mac UI is great (though, like iOS, not without warts) and the platform is worthy of your understanding and respect. The thing to do isn’t to wish there were navigation controllers and similar on Macs — instead, it’s to figure out what’s the best <em>Mac</em> version of your UI. Different APIs are the last thing to be concerned with: you’ll learn those. The harder part — and the interesting and challenging part — is designing a great Mac app.

<i>Update 4:40 pm</i>: <a href="http://log.maniacalrage.net/post/110289950079/inessential-uxkit-again">Garrett Murray follows up on his blog</a> with some great points:

>If I want to create a label, I’d love to create a UILabel (or, say, UXLabel) and know that by default it would perform in a logical way on all platforms. TableViews, animations, all of these core components would share a logical API you could use with little concern for how they behave and perform at the default level. Obviously, things like NSMenu would be on OS X only. That isn’t a deal-breaker for this. And sure, UXLabel might have some attributes available only on Watch. I think that’s all logical.
