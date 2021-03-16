@title The Hottest of All Xcode Tips
@pubDate 2021-03-16 11:41:59 -0700
@modDate 2021-03-16 11:41:59 -0700
It’s come to my attention that not everyone knows this. But everyone needs to know this.

In Xcode’s Organizer, in the Crashes section, you can right-click or ctrl-click on any row and choose Show in Finder. This will reveal a .crashpoint file — do a Show Package Contents and then dig in further. You will find .crash files with the full crash logs, which provide a lot more info than what you see in Organizer.

(Bonus tip: I just drag the .crashpoint package onto BBEdit, which shows the contents in its sidebar, where I can click on different .crash files. I assume other text editors have a similar feature.)
