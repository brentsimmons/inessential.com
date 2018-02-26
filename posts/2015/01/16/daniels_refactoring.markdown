@title Daniel’s Refactoring
@pubDate 2015-01-16 16:13:29 -0800
@modDate 2015-01-17 09:50:21 -0800
Daniel Jalkut wrote about <a href="http://indiestack.com/2015/01/same-tests-different-class/">his adoption of NSURLSession</a> — by writing a new cover class that has the same interface as his existing url-downloading code (which was a cover for CFNetwork).

This is the right way to do it. The callers — including the unit tests — don’t have to know anything about the implementation, since the interface is the same. That’s just good programming.

It’s also not how *I* would do it in this specific case.

My thinking:

It totally makes sense to have a cover class for CFNetwork, since it’s C-based but we want an Objective-C class. (I use <a href="https://github.com/ccgus/fmdb">FMDB</a> for a similar reason — so I don’t have to use SQLite’s C interface.)

But I don’t like wrappers for things that are already written in Objective-C. (I don’t like subclasses either, except in cases such as NSOperation and UIViewController that are designed to be subclassed.)

Instead, I’d rather just use a thing directly, rather than write a class that wraps a built-in class.

The difference may be subtle, so I’ll use an example. Consider an RSS reader that needs to download a bunch of feeds.

*Before* NSURLSession, I’d create an NSOperation subclass that downloads a feed. That subclass would use NSURL loading classes to download a feed and eventually call back somewhere with the result.

Now *with* NSURLSession, I’d create an NSURLSession and NSURLSessionDataTask objects to do the downloading. No NSOperation subclasses.

In *both* cases I’d have an outside class — RSDownloadFeedsSession or something like that — that would have an unchanging interface. But, importantly, RSDownloadFeedsSession wouldn’t be a general wrapper for NSURLSession. It would just be a thing (inherited from NSObject) that *uses* NSURLSession.

The goal, in other words, is to stay close to the frameworks. Because:

* Other people can understand my code more easily.

* I can understand other people’s code more easily since I speak the standard Cocoa dialect.

* I don’t have to worry about the curse of shared-code-that-wraps-things — that a change fixes App A but breaks App B. (Yes, unit tests may detect the breakage, but the point is to avoid the possibility of breakage.)

* I don’t have to worry about the other curse of shared-code-that-wraps-things — that it will accrete features and configuration and special fiddly bits until it’s difficult to maintain and no easier to use than the thing it wraps. (I’ve been down this road.)

But here’s a point worth making: every good programmer has their own style, the way that works *for them*. Which means that Daniel’s approach is utterly right for Daniel, as mine is for me. Part of the deal with becoming a good programmer is learning about yourself — learning what your style actually <em>is</em>, and being comfortable with it evolving over time.

<i>Update the next morning:</i> <a href="http://indiestack.com/2015/01/brents-feedback/">Daniel responds</a>. Daniel and I are doing things the same way more than not, which should not be a surprise.
