@title How We Fixed the Dreaded 0xdead10cc Crash
@pubDate 2020-02-13 13:40:22 -0800
@modDate 2020-02-13 13:40:22 -0800
NetNewsWire for iOS, [currently in TestFlight beta](https://ranchero.com/netnewswire/test-ios), was getting a *lot* of crashes related to background refreshing.

They would happen when the user wasn’t actually using NetNewsWire — it happened when the app would download feeds and sync in the background.

The crash logs were not identical, but they had this same thing:

	Namespace RUNNINGBOARD, Code 0xdead10cc

This meant that the system was killing the app because, after the background task was complete, the app still had references to a SQLite database (or sometimes another file).

We did everything we could to fix this over a course of several months, including various forms of major surgery — and the best we could do was make it *worse*.

I did a lot of research — including reading [this blog post](https://blog.iconfactory.com/2019/08/the-curious-case-of-the-core-data-crash/) from The Iconfactory several times — and we still came up with nothing.

Finally I asked around.

#### Advice

[Marco Arment](https://marco.org/) writes [Overcast](https://overcast.fm/), a podcast player, which is in some important ways similar to NetNewsWire: it downloads data from the web while in the background.

Marco had already been through all this with Overcast, and he gave me this advice:

> Don’t keep the SQLite database in the shared container. You’ll never get rid of all of those crashes. Instead, communicate with extensions via other means than having them read/write the DB directly, such as Darwin notifications or writing plist files in the shared container.
>
> iOS will always terminate the app and generate that crashlog whenever your app or extension has an open file handle to a file in a shared container at suspension time.
> 
> And there are some cases where your app gets forcibly suspended without calling background-task completion handlers. (Especially in extensions, where they don’t exist.)
> 
> I tried wrapping every SQLite query in a background task once to avoid this. A standard Overcast session may issue hundreds or thousands of database queries. I later found that apparently each one generates a process power assertion, the OS wasn’t made for that level of usage, and after some time, Springboard would crash.
> 
> There’s also the NSProcessInfo background-task thing that allegedly works in extensions, except that it doesn’t.
> 
> The moral of the story ended up being: just don’t keep your SQLite database in the shared group container. There’s no way to avoid these crashes 100% of the time.

We *were* sharing our SQLite database with one of our extensions! Marco’s advice is, basically, don’t do that.

So we stopped doing that. We un-shared the databases and switched to a super-low-tech thing for communicating between the extension and the app (the extension writes to a plist file which the app later reads).

And — as of [last night’s build](https://nnw.ranchero.com/2020/02/12/netnewswire-for-ios.html) — the dreaded `0xdead10cc` crashes are gone!

#### Continuing On

That was the last big challenge on our list for shipping. We still have work to do, but we’re getting close — the milestone says we have [just four bugs left](https://github.com/Ranchero-Software/NetNewsWire/milestone/4). Good deal.

PS I’ve since heard from other developers: don’t-share-the-database appears to be the common wisdom, which it just took me longer to learn. 🐥
