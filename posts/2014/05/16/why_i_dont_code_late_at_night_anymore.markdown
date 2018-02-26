@title Why I Don’t Code Late at Night Anymore
@pubDate 2014-05-16 15:46:59 -0700
@modDate 2014-05-16 15:48:45 -0700
I used to code until midnight, easily, most every night. Three and four a.m. were common.

But for the past few years my rule has been to stop at 10 pm. I break it sometimes, but going as late as 11 pm is fairly uncommon now.

One night a few weeks ago I broke that rule and wrote some code past midnight. Tested it quickly, called it good, moved on to other things.

#### A Crashing Bug

Then the other day I had a crashing bug that I just couldn’t believe. It was caused by trying to access beyond the bounds of an array.

That’s a mistake I *never* make.

And I read the code and it didn’t make any sense. How the hell could this be happening?

#### Details

I’ll explain what the code was doing.

• The sync server returns an array of noteIDs for notes that have been deleted.

• The current timeline view controller looks at those noteIDs and removes the corresponding notes from its array.

• It does that by 1) first figuring out the indexes of the notes-to-remove, then 2) removing those notes, via <code>removeObject&#8203;AtIndex</code>.

I know what you’re thinking — and I thought it too. I’ve been around the block long enough to know that you have to remove from an array in reverse order.

Duh. So here was my code:

<code>for (NSNumber \*oneIndex in [indexes reverseObject&#8203;Enumerator]) {</code><br />
<code>&nbsp;&nbsp;[notes removeObjectAtIndex:&#8203;[oneIndex unsignedInteger&#8203;Value]];</code><br />
<code>}</code>

I remembered writing that code late at night.

And there’s nothing wrong with that code. (Not exactly, anway — and those lines of code are unchanged even now.) See? I *can* code late night. Right?

But that code was where I was getting the beyond-bounds exception.

#### How Could That Be?

Some more details.

The sync server provides a list of noteIDs in no particular order. They might be displayed in any order in the timeline.

The indexes-to-remove might be something nice like [3, 6, 30, 65] — but it’s more likely they’d be in some random order like [30, 6, 65, 3].

It doesn’t really matter whether I loop through those indexes in reverse order or not — it’s going to crash when they’re not sorted.

Think about it: if there are 66 notes, and it removes note 3, then there are 65 notes (0-64), then removing note 65 will be beyond the bounds of the array, since the highest index would be 64.

(And when it didn’t crash it would be removing the wrong notes.)

I would have realized this had I been fresher when I wrote that code. But it was late, and I thought I was being smart. And I missed something.

#### The Fix

It was after 10 pm when I was working on the fix. I should have quit already and left it for the morning — but, sheesh, there’s no coding task I love more than fixing crashing bugs, and when I’ve got one by the throat I’m not going to let go.

Still, though. *After 10 pm.* I should have quit.

But I didn’t. And you know what I did? I fixed it. But the stupidest way possible.

I sorted the indexes before looping through them and removing notes from the array.

Well, it works, the code functions exactly as it should. It’s fine.

But why didn’t I think of <code>removeObjects&#8203;AtIndexes:</code>, which would have saved me all this hassle in the first place?

Because I really do need to stop at 10 pm. I may think I’m adding productive hours to my day — but I’m not. I’m writing bugs, or, at best, not the best code I could be writing. And I pay for it later.
