@title App wanted: crash log database and analyzer
@pubDate Mon Feb 23 11:43:36 -0800 2009
@modDate Mon Feb 23 11:45:52 -0800 2009
I wish I had an app that gathered crash logs for my apps.

It would store them in a database, provided a searchable and customizable user interface (desktop, browser, I don’t care), and, most importantly, allow me to write scripts that do automatic analysis, classification, and prioritization.

As an example: since my Mac app uses WebKit <em>a ton</em>, I get a fair amount of crashes with lines like this:

<code>Thread 0 Crashed:<br />
0   ...romedia.Flash Player.plugin</code>

(Yes, Flash, I’m complaining about Flash again. Flashy Flash crashes.)

When I’m looking at my crash logs, I’d love to be able to do a search with filters — to do something like “show me all crashes in the past week that are not Flash crashes.” I could write scripts that do pretty well at figuring out what’s a Flash crash and what isn’t.

At the same time, an app in beta right now has a crash with text like this:

<code>Thread 10 Crashed:<br />
...<br />
1   libxml2.2.dylib</code>

A crash like this means I’ve done something wrong with the XML parser: it should be top priority. Again, a script could figure this out. (By using logic something like, “if the crashing thread contains ‘libxml’ then set priority to highest.”)

This app would also give me the ability to mark crashes as fixed. In the example above, I’ve already fixed it — so I’d want to be able to mark that crash log as fixed, and have the app find all similar crash logs and give me the chance to mark all of them as fixed as well.

Maybe such an app exists and I just don’t know about it? I’ve thought about learning Python and doing it as a Django app (great excuse to learn Python and Django) — but if it already exists, or someone else wants to do it, then cool. (I do, after all, need to work on my other software.)

But one of the keys to this app is that there must be <em>no copy-and-pasting</em> of crash logs. It needs to be scriptable so that I can automatically add crash logs that come in via email or as files. If I have to spend <em>any</em> time getting things into the system, then it’s not worth it.

PS It would also do <a href="http://furbo.org/2008/08/08/symbolicatifination/">symbolicatifination</a> for iPhone crashes.
