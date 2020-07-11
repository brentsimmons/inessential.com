@title Imagining an Open Source SwiftUI
@pubDate 2020-07-11 12:00:20 -0700
@modDate 2020-07-11 12:03:45 -0700
Swift is open source and is used in more places than just Mac and iOS apps — it’s now appearing in places like [AWS Lambda](https://swift.org/blog/aws-lambda-runtime/), for instance.

But SwiftUI is not open source. At least not yet.

As a developer who uses SwiftUI, I’d sure <em>like</em> to see it made open source. I think there might be a good reason beyond just that, though — an open source SwiftUI could be made to work on other platforms.

Somebody would have to actually do that work, of course. But imagine that work has been done, and you can write SwiftUI code that runs on the web, Android, Windows, and Linux as well as on Apple devices.

Right now people are using web technologies and things like Electron to do cross-platform apps. And… it’s not great, and it’s hard to imagine Apple likes this situation. At all.

If SwiftUI makes it easier to make apps that work across Apple platforms only, that’s nice but not enough: the future will still belong to web wrappers like Electron.

The reason for that is simple. Apps cost a lot of money to make, and every additional platform costs yet more money.

The people who make the decisions on what to use aren’t generally the people who care about things like platform differences and performance. Those folks want to get the most bang for their buck, and so they’ll do what’s cheapest. Especially if you can’t *prove*, with data, the benefits of a native app over something like Electron (or other web wrapper).

(Bless those people. They are not Philistines as a rule — it’s just that they take their responsibilities seriously, as they should. They’re doing their job.)

But what if you could come to those people with an alternative — SwiftUI (and Combine) — and tell them that it will run everywhere, and that it’s at least as cheap as a web wrapper, and that it creates high-quality native apps?

That would be cool. I have no idea if that’s how people at Apple are thinking. But I hope they are.
