@title Vesper Testing
@pubDate 2014-06-15 16:28:15 -0700
@modDate 2014-06-15 16:30:37 -0700
I want nothing more than to dive into Vesper for Mac and write Swift code and work on a great Yosemite app — but I’m doing testing instead.

The server-side testing is wonderful. Almost everything is testable — and when a function isn’t easily testable, at least I can write a test for everything it calls. I totally get all the emphasis on testing I notice in the Ruby and JavaScript communities.

And I can even see why I might want to write tests *first*. (Maybe. Sometimes.)

#### Man, JavaScript, sheesh

I write JavaScript code like an Objective-C programmer. Say I want to change the parameters to a function — add one, change parameter order, whatever. I expect the compiler to tell me that now I have errors in every place where that function is called.

But, of course, that doesn’t happen. Sometimes I think I could do almost anything to my code and it would still compile. (Which marks an advancement in proficiency. At first it was a struggle to write JavaScript code that would compile at all.)

This happy-go-lucky compiler drives me *crazy*. But this is also where testing comes in — some one or more tests should fail after I edit parameters to a function. While that’s not as handy as the compiler telling me in the first place about errors and exactly what and where they are, it’s infinitely better than not knowing anything.

(And this is why I wish for Node.swift. Or for Mobile Services to support [TypeScript](http://www.typescriptlang.org/), which is, very roughly, JavaSwift.)

Testing isn’t *just* to catch errors a compiler would have caught, of course. But it does that too, and the more tests I have the less time I spend trying to figure out what just went wrong.

#### Man, GUI apps, sheesh

The other day — not in shipping code:

I fixed a bug. Released to beta testers. That bug fix caused another bug. I fixed that bug. Released to beta testers. That bug fix caused another bug. I fixed that bug. Released to beta testers. (It’s good now.)

Could I have written unit tests for any of these bugs? Nope. They were all in view controller code, and they required user input.

(Yes, [I’m aware that I’m wrong](https://developer.apple.com/library/mac/documentation/DeveloperTools/Conceptual/InstrumentsUserGuide/UsingtheAutomationInstrument/UsingtheAutomationInstrument.html). But creating and maintaining automated UI tests is such a pain still that I consider it not worth it. One day that may change.)

While the API server is about 2,000 lines of code and almost all testable, the iOS app is about 35,000 lines of code, and very little of it is testable.

Luckily, it’s possible to test the most critical parts: data migration and syncing. And I’ve written tests for these. But there are about 25,000 lines of UI code (estimated; I kind of think it’s higher) that need manual testing.

(Vesper is probably the smallest app I’ve worked on. And yet I still find myself staring at the project’s sidebar, looking for any way I can delete some code.)

So I’m spending today sweating vinegar as I try to control my impulse to get going on all the shiny new fun stuff — instead, I’m writing a many-hundreds-of-lines-long manual testing recipe. (Which I should probably have done a year ago, yes, but better now than going another year.)

I’ve broken it into two parts: pre-beta-release tests, and pre-App-Store tests. By the time I’m finished, the longer of the two should be pre-beta-release tests.

This is a <em>massively</em> boring thing to do. And it’s going to be boring to step through the recipe every time, too.

But you know what? Every one of those three bugs would have been found by my testing recipe, and they would never have been seen by beta testers if I had stepped through the tests.

If I’m not willing to buy quality with boredom, then I’m in the wrong business.

Well. Back to it. And after that it’s back to writing server tests. And then — then, finally — Mac app + Swift. My reward.
