@title The Clean Screen Habit
@pubDate 2016-06-03 12:27:09 -0700
@modDate 2016-06-03 12:27:09 -0700
I’ve spent years of my programming career on a team of one, and I ended up developing some idiosyncratic habits.

One of them could be called the “clean screen” habit. Here’s the scoop:

Xcode’s warnings and errors pane has to be clear at all times. If anything appears there, it has to be dealt with immediately. I enforce this in part by turning on treat-warnings-as-errors, so I’m forced to deal with everything.

Also: anything that appears in the Console pane must be dealt with immediately — that is, any message must be some kind of assertion failure or notification that something bad has happened. Otherwise it must be kept clear (with the exception of temporary caveman debugging).

Having these two panes clear tells me that the baseline health of the project is good. And it ensures that when something does appear, it’s an extraordinary event that I can’t miss — and can’t miss dealing with.

<p style="text-align:center">* * *</p>

You could argue that this is pointless and fussy. After all, this doesn’t do anything to prove that the app is well-architected or that I’ve chosen good algorithms or that it uses memory efficiently.

But that’s like saying showers are worthless because they don’t make you a snappy dresser. Cleanliness is just a start, but it’s a good and necessary start.
