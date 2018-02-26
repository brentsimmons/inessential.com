@title Mac Text Editors and Navigation
@pubDate Sun Nov 27 21:45:48 -0800 2011
@modDate Sun Nov 27 22:23:42 -0800 2011
I like native Mac text editors and use them all the time. I like that there are standard keystrokes that work the same in every editor.

But the hardest part of text editing remains text *navigation*. Moving around. Getting to the thing you want to edit.

#### What Vim gets right

Like <a href="http://www.vim.org/">Vim</a>, hate Vim, or *really* hate Vim, you’d look silly if you didn’t admit that it’s the king of text navigation. (But, seriously, I’m not suggesting you use it. I use it, but I’m a total weirdo. Touched. With issues. I work alone in a padded room.) 

Once you learn it, moving around in text becomes so intuitive-seeming and lightning-like that anything else is nearly unusable. You don’t even want to write email without it. (And you don’t have to, if you’re willing to use pine or Alpine or mutt.)

I do *not* need Mac text editors to emulate Vim. I’m not going to sell anyone on that, no way.

But there is one little thing they could do. And it wouldn’t hurt, and it wouldn’t change their Mac-like-ness at all.

#### Make Go to Line… fast and not-dumb

When you don’t have the rich (or insane, over-the-top) navigation control that Vim provides, you still usually have a Go to Line… command. That’s not a bad way to get around, not at all. I do it all the time.

Unfortunately, there’s no standard for Go to Line in Mac text editors. Each editor does it differently, and they usually screw up at least one part of it so that it’s not-particularly-usable. (Which causes me to curse through my nose, throw one of the plush toys they permit me to have, and then run back to Mama Terminal for solace.)

Here’s how Go to Line should work to make it usable for text navigation:

1. The small window that appears where you type the line number needs to be a window that opens without animation. It can’t be a sheet. It can’t be a big window. It can’t have it’s own custom animation. It has to be super-fast.

2. The insertion point must then be placed at the beginning of the gone-to line. The entire line must *not* be selected. (That’s a recipe for losing text if you’re an impatient and fast typist. Yes, there’s undo, but first there’s me saying ten hulk-smashes before I’m calm enough to continue.)

3. It should be obvious that it should also display line numbers (optionally, for people who want it).

It seems pretty simple.

#### How current editors handle it

Here are the mistakes made by various editors on my machine:

- <b>Xcode:</b> Big window. Selects entire line.

- <b>BBEdit:</b> Sheet.

- <b>TextMate:</b> All good.

- <b>Espresso:</b> Custom animation. Selects entire line.

- <b>Mail:</b> NO COMMAND AT ALL WHATSOEVER. MAIL, THIS IS WHY WE’RE NOT FRIENDS ON FACEBOOK.

- <b>TextEdit:</b> Selects entire line. Doesn’t display line numbers.

Only TextMate gets it right. BBEdit is very close — but I’d sure like to see that sheet change to a child window. (I’m a big BBEdit fan.)

I spend most of my time in Xcode, and that’s where, for me, this really should work properly. (I’ll file a radar! Yes! I will!)

#### Bonus: standardization

Apple has not suggested a standard for Go to Line. Editors use different keystrokes (cmd-L, cmd-J) and different commands (Go to Line, Select Line, Jump in [filename]).

This is one of those things that ought to be the same in every app. I’m all for innovation, but only when it’s different for an actual good reason. For no-brainer things — things like Go to Line — it ought to be the same, and it ought to be good, in every editor.

#### Double-bonus: link

I like <a href="http://www.moolenaar.net/habits.html">Seven habits of effective text editing</a> by Vim author Bram Moolenaar. It talks a lot about Vim specifically, but the lessons are general. Habit #1 is “Move around quickly.” Good article for people like me (and probably you) who edit text for a living.
