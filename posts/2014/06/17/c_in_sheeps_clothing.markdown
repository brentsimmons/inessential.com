@title C# in Sheep’s Clothing
@pubDate 2014-06-17 09:09:54 -0700
@modDate 2014-06-17 09:09:54 -0700
David Owens II has [some criticisms of Swift](https://medium.com/@owensd/swift-d3c212c35fd8). Swift is not exactly Objective-C without the C — it’s less dynamic, and more like C++ or C# in some respects.

(Via [Michael Tsai](http://mjtsai.com/blog/2014/06/17/swift-objective-c-without-the-smalltalk/). If you’re a developer, you need to subscribe to [Michael’s feed](http://mjtsai.com/blog/feed/).)

My suspicion: after a while, good Cocoa developers will use Swift most of the time, but we’ll have figured out the cases where using Objective-C makes sense. For instance: dealing with JSON, which is one of David’s examples, may be one of those places where Objective-C is the best tool for the job.

Maybe it’s like this: when things are orderly, Swift is perfect. When order needs to be made from chaos — such as when talking to web services — then Objective-C comes in to make order from that chaos, and then it passes off orderly objects to Swift code.

Experienced Cocoa developers will figure this out and won’t even have to think about when to use which language. The fact that we have both, and can use both languages in a single app, will come to be seen as a strength of the platform.
