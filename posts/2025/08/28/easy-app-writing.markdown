@title Writing Mac and iOS Apps Shouldn’t Be So Difficult
@pubDate 2025-08-28 10:26:28 -0700

In the ’90s and early 2000s I worked for UserLand Software — [Dave Winer](http://scripting.com/) was founder and CEO — on a Mac app called UserLand Frontier.

The app was a scripting system and hash-table-oriented database that powered the early blogging and podcasting worlds. (That sounds grand, but it’s probably an understatement — but this post isn’t all about Frontier’s impact on the web, so I won’t go into details.)

The app was implemented in two pieces:

* The *kernel*, written in C, implemented the database, networking, inter-application communication, various built-in data types, script compiler and evaluator and debugger, and so on
* The *scripts* used the kernel and implemented most of the actual app behavior

Since it was an app, it had plenty of UI — menus, contextual menus, buttons, larger UI components, and so on. What was brilliant was that you could, for instance, add and edit menus, and when you chose a menu command it would run your script. (Or when you clicked a toolbar button, etc.)

You could write an entire static blog publishing system and the UI to go with it without ever restarting the app. Click a thing, then see what happens in the app — and if it’s not right you’d edit the script, which would be automatically recompiled when called the next time.

In other words, there was absolutely no friction when it came to iteration. Write some code without restarting and see your changes immediately.

### How good was this really in practice?

You might imagine that we could do this for an hour or so before having to make changes to the kernel. Not so.

In fact, for the first three years I was there (might have been longer), I never even *saw* the kernel code. I worked all day every day as a professional developer at the script level, never having to restart the app. Just iterating like this all day long.

You might also imagine that the app was sluggish and slow since much of it was scripts instead of C code. It wasn’t! Scripts could be slow for the same reasons any code could be slow (I/O, of course, and algorithms and data structures not suited to the problem at hand) — but the app never felt slow.

I’ll remind you of the timing: *this was the ’90s.* We worked this way for real, and we were amazingly productive.

A scripting language plus key bits implemented in C was more than fast enough for an app. Even all those years ago.

### A scripting language built for productivity

I’m not writing this article to praise Frontier — I’m talking about it to make a point, which I’ll get to.

But I wanted to bring up a second aspect to this: it’s not just frictionless iteration that was so great, it was also the scripting language and environment.

One of the best parts of this was how easy persistence was. I mentioned the hash-table-based database. Hash tables could contain hash tables (Swift developers: picture a Dictionary inside a Dictionary, and so on).

(We just called them tables for short — but remember that these are hash tables, not tables in a SQL database.)

In any script, at any time, without any ceremony, you could read and write from the database simply using dot notation: `user.prefs.city = "Seattle"` would set the value of `city` in the `prefs` table which was contained by the `user` table. This value would persist between runs of the app, because it was stored in the database.

(You could also pass around addresses of things too — it was quite common to pass the address of a table to another script, so that the other script wouldn’t need to hardcode a location.)

It was utterly automatic. And it meant that while we did have to choose where in the database to store things, and how to structure our storage, we didn’t have to choose a storage mechanism. It was the database.

(Note: of course we could read and write files, and did so when necessary. But the point is that the database handled almost all our persistence and in a super-easy way.)

(Also note: the database had a UI. It was visible and browsable. You could and often did hand-edit it. Even the scripts lived in the database, and were addressable via dot notation, like everything else.)

### We had nice things!

I’ll say again — this was in the ’90s, more than 25 years ago, and it was a great way of working on an app.

I’m not saying apps these days need to be Frontier-like in any details. But it seems absolutely bizarre to me that we — we who write Mac and iOS apps — still have to build and run the app, make changes, build and run the app, and so on, all day long. In the year 2025.

And it seems retro in the worst way that we’re still using anything other than a scripting language for most of our code. We should be using something simple and light that can configure toolbars, handle networking callbacks, query databases, manage views, and so on. And maybe with a DSL for SwiftUI-like declarative UI.

Almost none of that code needs to be in a lower-level language like Swift or Objective-C. It really doesn’t. (I say this as a performance junkie!)

It could be in Ruby, Lua, Python, or JavaScript. Better still would be a new language invented specifically for the problem of writing apps, something designed to make the common challenges of app writing easier.

We did have this stuff decades ago. Not for app making in general, sure — but now it’s 25 years later, and a company like Apple could make this real for all its app makers.

It’s easy to see why things are the way they are right now, and you can point to a string of good decisions. No doubt.

But we can think outside of what we have now and ask: what would make app writing easier? What would make it a better experience? How could we get more done for our users with fewer bugs and faster turnaround?

I’m not saying that Frontier’s specific choices are the answer — I’m saying that the combination of frictionless iteration plus a purpose-built scripting language was extremely powerful, and we could use those things now.

And at some point I suspect these things are going to be table stakes for any platform that wants to attract developers. If you were a new developer right now, would you pick Xcode’s build-and-run, edit, build-and-run, edit — plus the growing complexity of Swift — over something like Electron and JavaScript?

### Random notes

Yes, I know about [PyObjc](https://en.wikipedia.org/wiki/PyObjC) and [RubyCocoa](https://en.wikipedia.org/wiki/RubyCocoa). Without first-class support in Apple’s developer tools, these were never going to work as popular alternatives.

I also know about (and use) Swift playgrounds and SwiftUI previews. Neither of these are as satisfying to use as I’d like, and neither of these are nearly as great as frictionless iteration in the actual app.

I also remember Xcode fix-and-continue, which didn’t work well enough to solve the problem of frictionless iteration. 

Anyway… One more thing about Frontier: we had a system where people could get updates to the app automatically via the web. Those updates were just serialized versions of scripts at various database locations, which would get unpacked and stored in each user’s database. (Those who opted-in, of course.) The app would not have to be restarted to get bug fixes and new features! And of course the updates were very small, since they didn’t include the entire app. This seems so futuristic, but we had this in 1999. Why couldn’t we have this now?

