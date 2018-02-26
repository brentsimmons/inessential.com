@title TapLynx 1.0
@pubDate Wed Oct 14 09:43:35 -0700 2009
@modDate Wed Oct 14 09:43:35 -0700 2009
<a href="http://taplynx.com/">TapLynx</a> is a framework for building media-based iPhone apps without needing to do any programming.

It’s a tool for developers, though — you still use Xcode to build the app. You configure it via a property list file, add artwork and feeds, build it, upload it. (You build a fully-native Cocoa app: it’s not like compiled Flash or something like that.)

Though programming isn’t required, you still <em>can</em> do some programming: a tab can have a custom view controller. An example case: you’re building an app for a sports team. TapLynx provides the news display, photo galleries, and audio and video. But you want a tab that shows scores and stats — that’s the tab that you write. But since TapLynx provides the other features, you can save time, make more money, and concentrate more on the part that makes your app special.

#### Some technical details

TapLynx is a static library. It’s a whole app in a static library. Since the views are things like UITableViews and UIWebViews, there’s no need for xib files. (I’m <em>not</em> anti-xib, by the way. But when a view is just a table — and it <em>needs</em> to be configured in code — a xib doesn’t make sense.)

The SDK provides a sample skeleton app that links to the library. The skeleton app has no code other than its main method.

The features, colors, feeds, and so on are all configured in a single property list file. Artwork is added to the Xcode project just as you would with any other project. There’s no black magic going on, in other words.

#### It’s 1.0

The future of TapLynx will be driven by the needs of developers. We can’t know in advance everything you’ll want and need, but we’ve had some experience building iPhone apps and we know what the basics are.

For instance, I’m sure you’ll need more programming hooks, ways to customize and add features via your own code. But I don’t know in advance what those will be. (The custom tab was obvious: the next step isn’t obvious.)

So we’ve set up a <a href="http://groups.google.com/group/taplynx">Google Group for TapLynx</a> as a place for feedback. I’d love to hear what would help you make apps faster, make your clients happy, and make you money.

#### It’s also for web developers

We’ve seen people build apps who aren’t Cocoa developers — or who hardly ever even use a Mac, let alone Xcode.

We quite definitely had website agencies and web developers in mind. For example: when specifying a color, you just use the hex value, as in #48EF93. We were thinking of you. :)

#### My favorite feature: over-the-air updates

When we were working with All Things Digital on their app, they wanted to have the same kind of immediate control over the app as they have over their website.

Well, in the world of iPhone development, we all know there’s no such thing as <em>immediate</em>. (At this writing, I’ve had a crashing bug fix — a two-line change — for NetNewsWire for iPhone in review for 10 days now.)

We came up with this: the config file that you edit to create the app can also be hosted on the web. The app will read that config file periodically (a period you can configure). Whenever there’s a new config file, it will re-configure itself.

This way you can add and remove feeds, change look and feel, etc. You might add a tab for a special event (Olympics, election, winter weather, whatever) and take it down later. Or add a photo gallery.

It even downloads the necessary artwork.

So you don’t have to do an App Store update and <em>hope</em> it gets up in time for the special event.

(It can’t download code, though, since that’s against the developer agreement with Apple. New code requires a new build and uploading to the App Store.)

#### A sort of homecoming

You probably don’t know this, but my experience before NetNewsWire was six years at UserLand Software where I worked on tools for developers and web publishers. I was there during very exciting days, during the early days of weblogs, during the development of RSS, XML-RPC, and OPML. I’ve been working with this same technology ever since.

But I forgot, until recently, how much I <em>love</em> doing developer tools. They’re fun to make — yes, totally — but even more fun is working with the folks who use them. It’s been coming back to me, and it’s like coming back to a great place I thought I’d never see again. (And some of the same people are there!)

#### Twitter

Yes, you can <a href="http://twitter.com/taplynx">follow TapLynx on Twitter</a>. 
