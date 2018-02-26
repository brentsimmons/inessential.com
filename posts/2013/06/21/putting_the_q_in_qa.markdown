@title Putting the Q in QA
@pubDate Fri Jun 21 12:58:25 -0700 2013
@modDate Fri Jun 21 13:09:27 -0700 2013
Here’s a bug in <a href="http://vesperapp.co/">Vesper</a>. You can reproduce this easily.

1. Start dragging a note from right-to-left to archive it.

2. Before you let go, take another finger and tap the hamburgrabber button in the top left to open the sidebar.

Note that the sidebar opens and the note is still in a partially-dragged state. That shouldn’t be, but I didn’t think of it when I was writing the code.

You can figure out why the bug exists. When I’m writing a feature, I don’t necessarily think of all the interactions with all the other features. I *try* to, but it’s easy to get overly-focused.

It’s also easy to miss bugs that are hard to hit in the simulator. (I don’t know how to reproduce this bug in the simulator.)

Here’s where our man <a href="http://www.neglectedpotential.com/">Nick Arnott</a> comes in. He does QA for Vesper and for <a href="http://www.doubleencore.com/">Double Encore</a>.

Nick does excellent work.

Which means that when I’m busy and have a lot to do, I curse his name, the air he breathes, and everybody who’s ever been nice to him. I suspect his heart is black and terrible and full of hatred toward me personally.

Which is just to say, again: Nick does excellent work.

During my recent talk at <a href="http://altwwdc.com/">AltWWDC</a>, I was asked what makes a good QA person. I think I said, “Doggedness.” Which in my personal lexicon is high praise. (When I think about my own abilities, I know full well that they exist only because I keep chasing sticks and don’t ever stop, not out of any innate talent.)

Here’s the thing about Nick: I think he’s convinced that there’s another bug. And he’ll keep going till he finds it. And, once he finds it, he’s convinced that there’s another bug.

He uses multiple fingers (I like to imagine he has a severed hand he keeps warm just to use for this) and takes a phone call and notices every deranged pixel. Then he writes good bug reports with steps-to-reproduce, often with screen shots, sometimes even with video.

That’s what makes a good QA person. The best are macabre figures who delight in torturing developers, but then make up for it with the succinctness and precision of their bug reports.

I suspect there’s a reason that he chose to be <a href="https://twitter.com/noir">@noir</a> on Twitter.
