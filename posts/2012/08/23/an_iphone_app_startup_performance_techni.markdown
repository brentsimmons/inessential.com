@title An iPhone App Startup Performance Technique
@pubDate Thu Aug 23 17:21:07 -0700 2012
@modDate Thu Aug 23 17:23:44 -0700 2012
In <a href="http://itunes.apple.com/us/app/glassboard/id453661198?ls=1&mt=8">Glassboard 2.2 for iPhone</a> (released yesterday) I used a technique for reducing startup time that is worth writing up.

#### The Three Phases of Startup

A table-based, data-driven app like Glassboard goes through three states:

1. <strong>Loading.</strong> System loads the app. It displays Default.png, and there’s no interactivity.

2. <strong>Loaded-but-useless.</strong> App is loaded. UI is displayed. But there’s no data yet — the data still has to be fetched.

3. <strong>Loaded-and-useful.</strong> Data has been fetched and displayed. The app is ready to use at this point.

Users don’t really distinguish between #1 and #2. If the first step is fast, but the second step is slow (or vice versa), your app won’t get a pass: both steps need to be fast, because the user is waiting for #3, for UI <em>and</em> data.

#### How I Made Step #2 Fast

(If you’re a veteran Cocoa developer, you already know how I did it, and you can skip reading this article.)

I assume you know how to make step #1 fast. (In general: run the minimum amount of code, avoid memory allocation, don’t block the main thread ever. If your main screen is just a table, don’t bother with a xib. Profile to figure out what’s really slow.)

After I optimized app-loading, I wanted to get the data loaded so fast that there was no delay between loading and loaded-and-useful. I wanted to wipe out step #2.

There was no way I could optimize the SQLite fetches to be fast enough to make that happen. (It needs to fetch messages and comments and their related boards and people.)

I needed a way to cheat.

I reasoned this way: the app would show the data that was current when you last quit the app. Yes, there would have been changes on the server since then — but those would have to be downloaded regardless.

So whether I fetched from the database or cheated in some way, the end result would be the same: the app would show the data from when you last quit. (Until downloads complete with new and updated data.)

I remembered a technique I had used in some old version of NetNewsWire for iPhone, which was developed on much slower hardware.

#### The NetNewsWire Solution

NetNewsWire displayed an outline of feeds with unread items. Creating that outline was very, very slow. It could take several seconds on the iPhones of that era.

There was no way I could let startup be delayed several seconds — that would have been monstrously bad. So what I did was cache just enough info on disk to be able to rebuild the outline without hitting the database.

I don’t remember if I used NSCoding or a custom plist-based serialization — but it’s the same concept. I saved the outline on disk periodically, and at startup read that file to create the outline.

#### The Glassboard Solution

I did the same thing here: I cached the data on disk. The messages displayed in that table are stored in a single array in the app, and I used <a href="https://developer.apple.com/library/mac/#documentation/Cocoa/Reference/Foundation/Classes/NSKeyedArchiver_Class/Reference/Reference.html">NSKeyedArchiver</a> to serialize it and <a href="https://developer.apple.com/library/mac/#documentation/Cocoa/Reference/Foundation/Classes/NSKeyedUnarchiver_Class/Reference/Reference.html">NSKeyedUnarchiver</a> to de-serialize it. I made the serialized versions of the objects also contain just enough info about related people and boards to create those as well.

This meant adopting the <a href="https://developer.apple.com/library/mac/#documentation/Cocoa/Reference/Foundation/Protocols/NSCoding_Protocol/Reference/Reference.html">NSCoding</a> protocol for several of my classes (statuses, boards, and people). (Since I’m not using Core Data — for good reasons worth writing up, and different from <a href="http://inessential.com/2010/02/26/on_switching_away_from_core_data">last time</a> — this was easy.)

When serializing, creating the NSData object to write to disk is separate from actually writing the data. The app creates the NSData on the main thread (via <code>-[NSKeyedArchiver archivedDataWithRootObject:]</code> — which is so fast you’d never notice. And then it writes the data to disk in the background, inside a <a href="https://developer.apple.com/library/mac/#documentation/Performance/Reference/GCD_libdispatch_Ref/Reference/reference.html">dispatch_async</a> block.

When de-serializing at startup, the NSData is read from disk and the objects are instantiated via <code>-[NSKeyedUnarchiver unarchiveObjectWithFile:]</code>.

I tried two different times:

1. As part of startup.

2. Right after startup.

Right-after-startup meant there was a perceptible, though very small, delay between app-loading and loaded-with-UI-and-data. The whole point of all this was to get rid of that delay.

But I was worried that de-serializing as part of startup would be too slow — I might get rid of that delay but at the cost of longer app-loading time.

I tried it.

And it was so fast it had no perceptible effect on app-loading time, and it got rid of that delay between app-loading and loaded-with-UI-and-data.

I got what I wanted.

#### Seeing it in Action

If you have Glassboard 2.2, kill the app (double-tap the home button, tap-and-hold on the app till it shimmies, tap the - button) and re-launch it.

You’ll see a couple seconds of the Default.png file (which is unavoidable), and then the actual UI and the data will load at the same time.

#### Obvious To-Do Item

But note what I still have to do — the avatars load <em>after</em> the messages. I don’t mind if they’re not ready immediately, but they should appear much more quickly than they do.

I don’t know yet how I’m going to solve this. But it has an interesting component to it: I only need those avatars that are visible right away. That simplifies the problem.

I’m not sure that NSCoding is the way to go here, since image data can be large. (Even small images can be surprisingly large, since we’re on retina displays.)

But you can bet two things: 1) there’s a solution, and 2) I’ll be obsessed with the problem until I figure it out.
