@title Open Source: DB5
@pubDate Thu Jun 27 09:33:52 -0700 2013
@modDate Thu Jun 27 09:33:52 -0700 2013
[DB5 is up on GitHub.](https://github.com/quartermaster/DB5)

I’ve mentioned, and my co-workers have mentioned, that we used a plist file to specify numbers, colors, fonts, and so on for [Vesper](http://vesperapp.co/). We did it this way because I wanted my designers to have authority *and* control.

I didn’t want them to have to ask me to change a color, or nudge a button a few pixels, or change a font. I’d rather they do it themselves – but I didn’t want them to have to dig through the code.

One option, of course, would have been to use Interface Builder to do layouts and set properties. But so much of the app is dynamic that we ended up using xibs for the Credits screen only. And, frankly, Interface Builder is a bit difficult, and it doesn’t have slots for every value we needed to specify.

So, instead, I gave them a single plist — DB5.plist — to edit.

The great thing about this is that they could edit, build, see the results, and continue. They could iterate quickly, and they had just one file to deal with. Editing a plist isn’t pretty, but it’s *easy*.

The code behind this is quite simple. Anybody could have written it, and I’m sure lots of people have written things very similar. We claim no revolution here — but we do claim that this little tool is great for our workflow. It’s one of the reasons we were able to collaborate so well and make a good app in just a few months.
