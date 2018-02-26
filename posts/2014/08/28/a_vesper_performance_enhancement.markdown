@title A Vesper Performance Enhancement
@pubDate 2014-08-28 15:27:48 -0700
@modDate 2014-08-28 15:32:03 -0700
<a href="http://vesperapp.co/appstore">Vesper 2.003</a> came out earlier this week — and it includes a syncing performance enhancement which I thought I’d write up.

Performance enhancements aren’t always as straightforward as the one I’m about to describe. Often they require the hard work of revising the data model, adding caching, or doing your drawing the old-fashioned way (as opposed to just setting a property on a layer, for instance).

This one happens to be easy to write about, so I will.

But first I’ll say that Vesper is already fast and gets plenty of praise for its performance. I’m a speed freak with zero patience — except for the considerable patience required to make sure my software works for people like me.

So this performance enhancement isn’t something that any current users are likely to notice, but it will become important in the future as people create more and more notes.

<p style="text-align:center">* * *</p>

Here’s what we noticed: the initial sync on a new device, with a large number of notes (more than almost anybody has; more than I have), seemed unexpectedly slow.

My first thought was that the server was having trouble handling this. It wasn’t — it was returning all the data quite quickly with no complaint. And the amount of data was around the same as a typical image file. A lot, sure, but not an insane amount for a first sync.

So I ruled out the server, networking, and JSON translation as issues. Next I did some poor-man’s profiling — I hit the pause button in the debugger a few times as the app was syncing.

And the same function always appeared: `getUniqueID`. It’s a little C function that calls `SecRandomCopyBytes` to generate a random unique ID for a note (VSNote object).

The answer was clear: that function either needs to get faster, or we need to not call it so often. Or both.

#### Not Call It So Often

The syncing system creates a VSNote object for each JSON note pulled from the server that does not exist locally. On first sync, that’s every single note.

The problem: VSNote’s init method generates a unique ID by calling `getUniqueID`. This is superfluous in the case of notes coming from the server — those notes already *have* a unique ID.

So I did the obvious thing: I created an `-initWithUniqueID:` method that allows the creator to specify a unique ID, which means I could avoid all those calls to getUniqueID.

Awesome. Problem solved. Done.

I could have stopped there, but I didn’t.

#### Make the Function Faster

It still bothered me that that function was so slow. It didn’t really matter, at this point. But why would `SecRandomCopyBytes` be so slow? Something like that could be a *little* slower than some other system APIs, but still the numbers I was getting seemed weirdly super slow.

So I did a straightforward timing test, and `SecRandomCopyBytes` itself is plenty fast enough. What gives?

I thought it might be the collision check. There’s an NSMutableSet of all note unique IDs, and we check the returned value of `getUniqueID` to make sure it’s not in that set. Profiling told me that that’s not the slowdown. (As expected, since the collision check happens in getUniqueID’s caller, not in the function itself.)

What I found was that it was the *limits* on unique IDs that were causing the problem.

The limits are this: it has to be a positive 53-bit integer (instead of 64-bit), and the integer has to be greater than the constant VSTutorialNoteMaxID. (Which is 100.)

The body of `getUniqueID` is actually a loop. It calls `SecRandomCopyBytes` repeatedly until it gets a uniqueID that fits within the limits.

I had thought, naively, that it would typically take one to three calls to get a suitable uniqueID — but I was wrong. Ten passes through the loop wasn’t that unusual, and it could be more.

The solution here was pretty simple: if the number is outside the range, use some arithmetic to get it inside the range.

If it’s negative, subtract it from zero to make it positive.

If it’s greater than the 53-bit limit, divide in half. (In a loop until it fits within the limit.)

If it’s less than VSTutorialNoteMaxID, add VSTutorialNoteMaxID.

This made it so that getting a unique ID that fits within the limits takes exactly one call to `SecRandomCopyBytes` instead of potentially many calls.

There is still the possibility of collision with an existing ID, but that would be so rare (most likely never), and the consequences are just a second call to `SecRandomCopyBytes`, so I didn’t worry about that.

But, again — most performance issues I run into don’t have nice straightforward solutions like this one. When they do, I don’t mind. It used to be that I’d beat myself up for not doing this better the first time, but these days I don’t. I’m just glad that I learned something and made the software better.
