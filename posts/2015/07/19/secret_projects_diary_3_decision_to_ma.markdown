@title Secret Projects Diary #3: Decision to Make
@pubDate 2015-07-19 16:21:01 -0700
@modDate 2015-07-19 16:21:01 -0700
Both my secret-project apps are very dynamic. (They both even have plugin architectures, so that people besides me can extend the apps in significant ways.) The designs call for heavy reliance on protocols — protocols all over the damn place.

Now I’m faced with a decision. Even though there are solutions to <a href="http://inessential.com/2015/07/19/secret_projects_diary_2_swift_2_0_prot">my earlier post regarding Swift and protocols</a>, there are lots and lots of places that need solutions.

And those solutions require more code than I was expecting to write. More code means more code to maintain and more places for bugs to hide. And those solutions don’t have — I hate to say it — the elegance of Objective-C.

I was hoping that I could use protocols in Swift in much the same way I do in Objective-C. That is, just as Objective-C doesn’t care about the difference between `id<Foo>` and `ConcreteFoo *`, Swift wouldn’t care about the difference between `Foo` and `ConcreteFoo`. But that’s not the case.

<p style="text-align:center">* * *</p>

I feel like a putz every time I write “I’m going to use Technology X!” and later write “No I’m not!”

People tease me about it (which is fine).

But I’m not a curmudgeon. I’d never call myself a graybeard (despite the actual gray that appears when I skip a day shaving). I *like* new things.

Here’s the thing: I have a responsibility to choose the best tool for the job, knowing that the best tool is the best tool for me, at this time, on this specific job.

And I like writing about these decisions, on the grounds that my actual circumstances will be different from yours but that it’s good exercise to follow along with other people’s engineering decisions. (Well, I certainly get a benefit from reading what other developers write, at least.)

<p style="text-align:center">* * *</p>

Here’s one way to think about it: how much grief will I put myself through trying to get my protocol-heavy Swift code to work *and* make it good code and elegant?

<p style="text-align:center">* * *</p>

Here’s another way to think about it. If Objective-C didn’t have the ability to treat `id<Foo>` and `ConcreteFoo *` in the same way, and suddenly Swift had that ability, would we be talking about how this feature is really, really cool? A game-changer? The best thing since type inference?

I think so.

So is it smart to cast aside Objective-C, which already has this (and other) wonderful features, just because it’s not the new thing?

Except that it’s not just that Objective-C isn’t the new thing. It’s also not the *future* thing. Switching isn’t a matter of if but of *when*.

And I want these apps to last a long time.

<p style="text-align:center">* * *</p>

In the end, it took me writing it up to decide to stick with Swift.

Expect more blog posts.
