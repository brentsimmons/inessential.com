@title Why Reboot Frontier?
@pubDate 2014-05-31 16:19:37 -0700
@modDate 2014-05-31 16:27:23 -0700
In <a href="http://inessential.com/2014/05/24/what_happened_at_userland">What Happened at UserLand</a> I mentioned rebooting Frontier as a modern Mac app.

I got lots of email, including email from people I haven’t heard from since when I was at UserLand. That was cool.

Everybody has a different idea of what a new Frontier would be like.

There were some common themes. The big one: most people wanted the scripting language to be whatever they’re using now: Python, JavaScript, or Ruby instead of UserTalk.

People also assumed that what I was talking about was writing something like the version of Frontier that ran Manila, that could host tens of thousands of blogs on a single server.

Which made me realize that Frontier has several personalities.

It started out, after all, before the web, as a scripting system for Macintosh. Let’s call that Small Frontier.

In the mid-’90s came Medium Frontier, when Frontier gained web scripting tools and a framework for building static websites via scripts and templates.

Then in the late ’90s came Big Frontier, when it became a server, when it hosted those many thousands of Manila sites.

The question appears to be: which personality interests me?

#### The Real Question

But the real question is something else: what’s my goal? Why do I want to do this?

It can’t just be nostalgia or a sense of unfinished business. There *is* a reason.

In the ’80s and ’90s, in the Hypercard era, the original mission of the Macintosh was applied to developer tools. The world of GUI applications, which we take for granted now, was still new, and there was a sense that these applications could be a democratizing force.

People could experience the power of scripting without having to learn Unix and the command line. (Which Macs didn’t even have in those days.) Everything should be *visible*, point-and-clickable. A database is something you browse and edit in a GUI — it’s not some hidden service.

To me this is lovely. Lovely because, through the virtues of good GUI app design, it brings real power to anybody who wants it.

One of the early principles of the Macintosh revolution, the GUI revolution — making software development available to everybody — seems to be lost. But it shouldn’t be.

#### So Naive

Well, that was a lovely vision for the ’80s, but history has shown that people want to look at Facebook and cat videos. They don’t want to <em>make</em> things. You’re never going to turn regular people into programmers.

That’s fine. The point can’t be to get everybody in on the fun, because it would never happen. A modern Frontier is still a nerd’s tool.

But here’s my point: it *is* (or would be) more approachable than most of the tools we have now. There would be some people who get their start programming this way. There would be people building things they wouldn’t have built otherwise.

Some people. Not most people. Not 1% of all Mac users. Some small number.

#### It Can’t Just Be a Prometheus Complex

Is my motivation to bring the power of programming to people I’ve never met just because I’m a nice guy?

Well, sure.

But I have a political goal. <a href="http://dashes.com/anil/2012/12/the-web-we-lost.html">The web we lost</a> is my constant companion, my shadow friend sitting right next to me as I do everything I do.

While “rebooting Frontier” doesn’t show up on the list of things to do to <a href="http://dashes.com/anil/2012/12/rebuilding-the-web-we-lost.html">rebuild that web</a>, it’s on my personal list.

As the web has become so dominated by centralization and limitation, I want more and more to build my own little Molotov cocktail and toss it in the middle of it all. That’s what my shadow friend wants. That’s what this is.

In less-dramatic terms: my premise is that if I build a good, approachable, easy-to-learn GUI app that lets people experience the power of scripting the web, that will actually help.

After all, Frontier played a role in building that web in the first place.

#### But Which Personality?

What does that mean in practical terms? Small Frontier? Medium? Big?

Well, the small version didn’t have anything to do with the web. Medium Frontier is where my heart is.

One of the common things in the email I get about this is the idea of modularity. Frontier was always a monolithic GUI app and runtime, with an http server baked-in.

And there’s a good reason for this — that was part of what made it approachable. You didn’t have to install and configure a bunch of different pieces and do all the crazy things developers do. You just launch an app.

Here’s the thing about the modern world: it could still be a single app and be modular, as long as the various pieces can be separated out and rebuilt and repurposed for other things.

And — because computers have gotten so fast, and because of my own mania for performance and scalability — creating Big Frontier is just a side effect of creating Medium Frontier.

#### Starting at the Bottom

I don’t have a detailed design. I expect to feel my way along. I also expect not to finish — I have the suspicion that this is just something I like to think about, but in practice have trouble finding time to do. Disclaimer disclaimed.

I also expect to use other people’s work as much as possible. When Frontier was created, pretty much everything had to be done from scratch. That’s not true today.

The first step is obvious: the under-the-hood implementation of a hierarchical, schema-less database.

It should be a library that any app can use. It should have a scripting API. (I’m not sure of the mechanics of this yet. Research required.)

It might sound odd at first, but the plan is to build on top of SQLite. (And <a href="https://github.com/ccgus/fmdb">FMDB</a>.) Reasons: SQLite is incredibly stable. It’s fast. I have a decade of experience with it. And building a hierarchical database using SQLite isn’t that hard.

The database schema, as it appears right now: uniqueID, parentID, name, value, valueType, mimeType.

The API (still in progress) lets you do things like move and rename things. Get all children of a parent. Etc. Deletes are recursive — delete a table and all its descendants are deleted. Moving something is as simple as changing its parentID.

Changes to the database are reflected immediately (there’s no separate save). There’s an in-memory cache. The database is queried and updated in a background serial queue, but because of the cache much of the time you won’t have to wait for the database.

The idea is that anyone using the database has the simplest possible interface: just add, remove, and edit data via the API, and persistence is automatic.

There should probably be some way to make queries, too. (Perhaps using NSPredicate.)

I’ve written some code. Maybe 5%. If I get it close to completion, I’ll put it up on Bitbucket.

The step after that is probably a GUI app that browses the database and lets you make changes.

After that I’m not sure yet. Something something scripting. Don’t know. JavaScript? Seems like a modern choice, and I’ve been getting to know it. JavaScript is probably the closest to UserTalk, and it means I don’t have to write and maintain a scripting language.

Maybe other languages too? I’m a long way from having to think about it.

