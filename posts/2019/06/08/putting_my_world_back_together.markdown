@title Putting My World Back Together
@pubDate 2019-06-08 15:42:50 -0700
@modDate 2019-06-08 15:42:50 -0700
I have not watched WWDC videos so avidly, and with so much glee, in a decade. The last time was probably with the iPhone SDK.

And now I’m putting my world back together in my head, a little bit at a time. It’s going to take a while.

One thing you should not miss: the SwiftUI DSL is not some Apple-only magic. We can define our own DSLs in Swift 5.1. Imagine what more Apple can do with this, and imagine what *you* can do with this.

See the [What’s New in Swift](https://developer.apple.com/videos/play/wwdc2019/402/) video. Also pay close attention to property wrappers.

One thing I keep wondering about — because my apps tend to be about databases — is the SwiftUI of Core Data. In my app I use value types for most things stored in the database, which Core Data doesn’t support. So this means a whole bunch of custom code.

I would love to have defined my model using a Swift DSL and used an engine that (like Core Data) stores my data in SQLite.
