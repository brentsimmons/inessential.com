@title Frontier Diary #2: Two Good Ideas that Aren’t Good Anymore
@pubDate 2017-04-11 13:01:55 -0700
@modDate 2017-04-11 13:08:30 -0700
Strings in <a href="http://inessential.com/2017/04/03/frontier_diary_1_vm_life">Frontier</a> are usually either Pascal strings or Handles.

You probably don’t know what I’m talking about. I’ll explain.

#### Pascal Strings

Frontier is a Mac Toolbox app that’s been Carbonized just enough to run on OS X. You may recall that the Mac Toolbox was written so long ago that the <a href="https://developer.apple.com/legacy/library/documentation/mac/pdf/MacintoshToolboxEssentials.pdf">original API</a> was in Pascal. That Pascal heritage lived on in many ways, even after everyone switched to C — and one of those ways was Pascal strings.

A Pascal string is n bytes long, and the first byte specifies the length of the string, which leaves the rest of the bytes for the actual string. `Str255` was probably most common, and certainly is most common in Frontier, but there are also smaller sizes: `Str63` and `Str31`, for instance.

Unlike C strings, they’re not zero-terminated, since there’s no need to calculate the length: you always know it from that first byte.

You create a literal Pascal string like this…

	Str255 s = "\pThis is a string";

…and the compiler turns the `\p` into the correct length (16 in this case).

Now, I bet you’re saying to yourself, “Self, those Pascal strings are too small to be useful.”

But consider this: every menu item name can fit into a Pascal string. You can fit a window title or a file name into a Pascal string (in fact, memory suggests that file names were even shorter, were `Str31` Pascal strings). Any label or message on any bit of UI is probably short enough to fit into a Pascal string. (Especially if you assume English.)

So for GUI apps these were terrifically useful, and the 255-byte limit was no problem. (You can fit a tweet in a Pascal string, after all, with a bunch of room left over. [Well, depending on the size of the characters.])

Frontier still uses them internally a ton. (For some reason, in the Frontier code, `Str255` strings are called `bigstring`, which sounds ironic, since they’re so small, but I think it was to differentiate them from even smaller Pascal strings such as `Str31`.)

You might ask what the text encoding was for these strings.

“Text whatzit?” I’d reply. “Oh, I see. Just regular.” (<a href="https://en.wikipedia.org/wiki/Mac_OS_Roman">MacRoman</a>.)

It was a good idea, but its time has come and gone. We have better strings these days.

#### Handles

Frontier includes a scripting language and a database, which means it certainly has a need for strings much larger than 255 bytes.

It also needs heap storage for other things — binary data, structs, etc. — that could be much larger than 255 bytes.

Enter the Handle. A Handle points to a pointer *that might move*: the memory you access via a Handle is *relocatable*.

Which sounds awful, I know, but it was a smart optimization in the days when your Mac’s memory would be a single-digit number of megabytes, or even less than that.

Here’s the problem: your application’s heap space can become fragmented. It could have a whole bunch of gaps in it after a while. So, to regain that memory, the system could compact the heap — it would remove those gaps, which means relocating the memory pointed to via a Handle.

This is better than running out of memory, obviously. But it means that you have to be careful when dereferencing a Handle: you have to actually lock it first — `HLock(h)` — so that it can’t be moved while you’re using it. (And then you unlock it — `HUnlock(h)` — when finished.)

Handles are also resizable — `SetHandleSize(h, size)` — and resizing a Handle can result in it needing to move, if there’s not enough space where it is. Or other Handles might move. You don’t ever know, and don’t care, and you think this is elegant because the system handles it all for you.

All you have to deal with is an additional level of indirection (`**h` instead of `*p`), locking and unlocking it when needed, and disposing of it — `DisposeHandle(h)` — when finished. (No, there’s no reference counting, slacker.)

Nowadays, on OS X, Handles don’t ever move and there’s no heap compaction. So there’s no reason for them whatsoever. And they are, as expected, deprecated.

Nevertheless, Frontier, a Mac Toolbox app written in C, uses Handles everywhere.

(I remember being shocked, when I first started learning Cocoa 15 years ago, that there were no Handles. It seemed *incredibly* daring that objects were just pointers. It made me nervous!)

#### The Size of the Job

Almost all the Mac APIs that Frontier uses are deprecated. That’s one thing.

But it’s worse than just that: the ways Frontier handles strings and *pretty much every single thing it stores on the heap* are also deprecated.

So: what to do?

The end goal is a Cocoa app, which means I’ll be able to use Foundation, CoreFoundation, and Swift data types: NSString and Swift String, for instance. There are a number of different structs in the code, and those will be turned into Objective-C and Swift objects and Swift structs.

The tricky part, though, is getting from here to there. I think the first step is to start with Objective-C and Foundation types and use them where possible. I can do that without actually turning it into a Cocoa app (the app will still have its own WaitNextEvent event loop and Carbon windows) — which means I’ll have to bracket all Objective-C code in autorelease pools, and I’ll have to use manual retains and releases. I’m not sure how far that will get me, but it will get me closer.

PS Here are a couple articles by Gwynne Raskind on the Mac Toolbox you might enjoy: <a href="https://mikeash.com/pyblog/friday-qa-2012-01-13-the-mac-toolbox.html">Friday Q&A 2012-01-13: The Mac Toolbox</a> and <a href="https://mikeash.com/pyblog/the-mac-toolbox-followup.html">The Mac Toolbox: Followup</a>.
