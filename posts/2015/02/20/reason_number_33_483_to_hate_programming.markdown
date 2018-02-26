@title Reason Number 33,483 to Hate Programming
@pubDate 2015-02-20 15:26:31 -0800
@modDate 2015-02-20 15:30:30 -0800
In one of the several apps I work on, I have a controller class that runs into a solution like this:

While the app is quitting, and things are being torn down, the controller class runs code it doesn’t need to run — because it watches for notifications of various types and does things. And code from elsewhere calls into the controller class for the same reason.

Well, that code *shouldn’t* run at app-quit time, since it’s extra work that doesn’t need to happen. And, worse, the object graph can be in a weird, partway-torn-down state, and any work done then could cause a crash.

The non-beautiful but acceptable and expedient solution was for the controller class to watch for the app-will-terminate notification and set an internal property (appIsTerminating) to YES when it gets it.

A few methods that I know for sure shouldn’t run at app-quit time (because they update the display) then return early when self.appIsTerminating.

This makes quitting faster, and some crashing bugs are avoided. And there are maybe 10 new lines of code.

(A better solution involves an audit of a bunch of code and a bunch of thinking and testing. Several days of work in this case. Possibly a week. Not worth it.)

#### But Here’s Where Things Get Ugly (or Uglier)

That controller class has a couple subclasses. Without those subclasses the parent class would have a bunch of nasty switch statements. Not good. Those subclasses are needed. (I like to avoid subclasses as much as possible, but there you go.)

But then I found that one of the subclasses also needs to know when the app is quitting — for the same reason of avoiding work at app-quit time. How should I do that?

It could register for the app-will-terminate notification also. With the same selector, and then have that method call super? I don’t think I’ve ever written a notification handler that called super. That means declaring it in the .h file for the superclass. Erg. (And never mind that the notification handler would be called *twice*, since superclass and subclass both register for that notification — which wouldn’t hurt anything, but smells bad.)

Or the subclass could *not* register for the notification, but know that the superclass does, and implement the notification handler (and still call super inside the notification handler). But then the subclass knows a weird secret about the superclass. (Sure. It already does know a few secrets. But I prefer to write my subclasses as if they don’t know anything about super’s implementation.)

Or I could have the superclass expose the appIsTerminating property in its header file, so that the subclass could see it. This also sucks, because a controller class has no business exposing its own copy of global application state.

In the end, though, that’s what I did. (Along with a comment that the property was there for subclasses.)

It reminds me that there are two competing values:

1. Do everything the right way every time.

2. Make responsible and professional decisions about time and expenses and benefits and drawbacks.

This is a super-small thing. The code I added is clear and obvious, and there’s very little of it.

But still it makes me <em>itch</em>. I did this work a few days ago and I went to bed last night thinking about it. (And out pops a blog post the next day.)

There are times when I think I’m way too fussy. There are times when I think I’m not nearly fussy enough. Often those are the same times. I don’t know which is correct.
