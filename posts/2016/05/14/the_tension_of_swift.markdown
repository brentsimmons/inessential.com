@title The Tension of Swift
@pubDate 2016-05-14 09:47:56 -0700
@modDate 2016-05-14 09:47:56 -0700
Let’s get this out of the way first: I write new code in Swift, both at Omni and in my personal projects, and I’m positively bugged when I have to write Objective-C code.

But Swift makes me anxious for the future, and I think I know why.

It appears to me that the Objective-C runtime will not appear everywhere Swift appears, and it also appears to me that the Objective-C runtime’s days are numbered everywhere. (I hear some of you clapping.)

But the Objective-C runtime allows AppKit and UIKit to provide some powerful features that I’d hate to do without: the Responder Chain, xib and storyboard loading, KVC, and the undo manager.

If you’re writing a Mac or iOS app — even if all your code is in Swift — you rely on these features.

<p style="text-align:center">* * *</p>

At a lower level these depend, at least conceptually, on a few things:

1. `respondsToSelector` — can you send a given message to a given receiver?

2. `performSelector` — actually send a message, with arguments, to a given receiver.

3. String to Selector conversion.

4. String to Class conversion.

(Did I miss anything big?)

You do have these things in Swift — but, importantly, only with NSObject-based objects. Only with the Objective-C runtime.

<p style="text-align:center">* * *</p>

What makes me nervous is Swift’s emphasis on type safety and on compile-time resolution. As long as we also have what we need from Objective-C, then that’s fine — then we still get xibs and storyboards, the Responder Chain, and so on.

But when I read the writing on the wall, I read that that’s not a permanent position. (I could be wrong.)

What’s the replacement, then? How, in other words, do we retain major features that app writers rely on unless Swift itself grows to include those dynamic features from Objective-C?

I have to think that that’s what Swift 4 will be about. If Swift 3 is about building a beautiful language (and I think it is), then Swift 4 should be about standing it up to the needs of app writers, so that it’s not forever tied by the leg to the Objective-C runtime.

I’m nervous. I have some faith, but I’m still nervous. Should I not be?
