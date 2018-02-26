@title Apology
@pubDate 2014-02-03 22:14:08 -0800
@modDate 2014-02-04 15:32:23 -0800
I’m sorry for being a snarky jerk the other day on Twitter.

[I wrote](https://twitter.com/brentsimmons/status/429790796397547521):

>“Xcode cannot handle our scale” is the new day and night phones.

The “day and night phones” part refers to [Dave Morin’s infamous interview](http://www.vanityfair.com/culture/my-phone/2013/03/dave-morin-path-facebook-apple). If you’ve never read it, you should. It’s funny.

The “Xcode cannot handle our scale” part refers to the recent [Q&A on Quora about the new Facebook app Paper](http://www.quora.com/Facebook-Launches-Paper-January-2014/What-was-it-like-to-help-develop-Paper/answer/Jason-Barrett-Prado).

My comment was undeserved, and it was beneath me, and I apologize to the Paper team without reservation.

<p style="text-align:center">* * *</p>

Though I haven’t used Paper myself (I don’t have a Facebook account), I’ve heard from people whose taste I respect that it’s a remarkable achievement and an excellent app. So not only do I apologize, I also congratulate the team.

<p style="text-align:center">* * *</p>

Nevertheless, I’m still interested in the details here. Why would an iOS app with a complexity presumably much less than GarageBand (for instance) be of a scale hard-to-handle in Xcode?

There *are* apps that Xcode can’t handle, or can’t handle well, I’d bet, though I’ve not seen this with my own eyes. It’s easy to imagine that Photoshop, Microsoft Office, and Chromium are very difficult to handle in Xcode. I don’t know this for a fact, but I’ll stipulate it.

Facebook iOS developer [Grant Paul tweeted](https://twitter.com/chpwn/status/429918584337207298):

>@brentsimmons @alanzeino @ashfurrow For example, Paper has ~100 projects in the workspace. Takes 45+ seconds to open on a high-end rMBP.

That sure sounds like Xcode can’t handle Paper’s scale: 45 seconds is ridiculous. I imagine that other operations are similarly slow.

I would have started breaking Paper into separate workspaces when it hit about six projects. Or fewer. I’ll call that a matter of personal style, though, and not claim it as a best practice.

But the question in mind is this: why are there about 100 projects in the workspace?

<p style="text-align:center">* * *</p>

I don’t know why. I have some theories, which may be true in some combination. Or may not be at all true.

Perhaps they have every line of iOS code they’ve ever written all in those projects. The Quora page suggests as much: Paper “lives in the codebase of the other mobile apps at Facebook that has hundreds of regular contributors.”

Another possibility: they’re re-implementing UIKit, or parts of it. From the Quora page:

>The engineering complexity here is finding a way to fully utilize the multicore architecture of newer iPhones on top of the UIKit framework which has no support for multithreading. Significant work went into creating a framework for doing rendering work on multiple threads, and we spent a long time finding the balance between performance and complexity. Turning synchronous operations into asynchronous ones adds a lot of cognitive overhead, and this was one of the biggest challenges of the project.

I don’t know why this is so complex or challenging. Between operation queues and blocks, doing rendering work on multiple threads is just not that hard these days. I’m far from the only developer who’s been doing this long enough to be extremely comfortable with it.

But I don’t know the details, and that makes all the difference.

It’s also possible that they’re using a ton of external libraries.

[Sam Marshall tweeted](https://twitter.com/Dirk_Gently/status/430467177930428416):

>@alanzeino @dannolan php, chromium, webkit, zlib, libjpg, JSONKit, yaml, yasm; all licenses cited in the Paper license file. Why on earth.

If it’s true that the workspace includes the code from a bunch of external libraries — including some huge ones — then I don’t know what to think. Why not, for instance, use the system-supplied JSON parser?

Well, the answer might be that there are bugs in Apple’s code. (There certainly are.) Or it could be that they need more than UIWebView provides, so they have a private build of WebKit. I don’t know. I’m speculating.

<p style="text-align:center">* * *</p>

Here’s the thing: even if there’s a good reason for every one of those 100 projects, there’s no good reason to need 100 projects to build almost any iOS app. (Maybe GarageBand.)

“Xcode can’t handle our scale” should almost always be considered a signal from Xcode that the workspace needs major surgery, because at that point you have a workspace that an individual developer can’t handle either. (Particularly for iOS apps. MacBU and Adobe can ignore me on this point.)

But I don’t know the details — I’m totally guessing when it comes to the specific case of Facebook Paper. And so I can’t definitely say that this workspace is a sign of a problem with the code or the process.

Still, though. 100 projects. I’m massively curious. How did it happen, and what will they do next to deal with it?
