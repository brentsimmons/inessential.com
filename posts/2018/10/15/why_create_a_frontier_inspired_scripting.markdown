@title Why Create a Frontier-Inspired Scripting App?
@pubDate 2018-10-15 22:28:35 -0700
@modDate 2018-10-15 22:46:10 -0700
Let me tell you about Frontier.

It still runs (though on its last leg as a 32-bit app), but I’ll talk about in the past tense, because I’m talking about it in its heyday in the ’90s and early 2000s. I was working at UserLand — [Dave Winer](http://scripting.com/)’s company, which made Frontier — at the time. I was a Frontier enthusiast *before* I joined the company. It was my dream job.

Frontier began life as a Mac scripting app, before even AppleScript. While it never lost that ability, it turned into a *web* scripting app around 1995, which is when I first started using it.

In those days — ’90s and early 2000s — Dave Winer invented, collaborated on, popularized, or fleshed-out a number of things we take for granted today: websites created with scripts and templates, weblogs, RSS, RSS readers, podcasting, OPML, and web APIs (XML-RPC).

It was an extraordinary run of creativity. You might just assume that Dave and his team were writing in Perl or Python or similar — but we *weren’t*. All this work was done in Frontier.

#### Does the tool matter?

It’s easy to say that the tool doesn’t really matter, that it was all about the people and that particularly fertile time. And it *was* about that.

But if the tool doesn’t matter, then why do developers care so much about their tools? Tools matter too.

Nothing in my entire career has ever matched Frontier for how it enabled me to make things quickly. Things that are difficult in other environments — persistence, debugging, *seeing* the results of a script — are so simple in Frontier. It’s just how the app works. It still feels to me like it comes from the future.

The bet I’m making is that there was something special in this design, that this particular tool was capable of unleashing a level of creativity capable of changing the tech world.

#### What Frontier Was Like

Frontier was a Mac app (yes, there was a Windows port eventually) with an integrated [hierarchic database](https://en.wikipedia.org/wiki/Hierarchical_database_model) and scripting system.

The key is that it was a *Mac* app, in the very best sense — it had that old-school Mac philosophy of taking things that were abstruse and difficult and reserved for the priesthood and giving them an easy-to-use GUI. You browse the database and add, edit, and delete values. Everything lives in the database. 

Even your scripts live in the database. Open a script in a window, edit it, click Run or Debug, jump to a different script, etc.

#### The database

Think of the database like a dictionary that could contain dictionaries. We call those *tables*, but they’re not at all tables in the SQL sense. (Think hash table.) A table can have subtables, and sub-subtables, and so on.

The database holds scripts, outlines, menubars (you can create menus and attach scripts to menu items), styled text, strings, arrays, booleans, numbers of various types, binary data, and more. (Even some things nobody uses anymore, such as QuickDraw rectangles.)

There’s one simple bit of power — it sounds small to say it, but it’s huge: persisting data from a script is as simple as this:

<code>states.Nebraska.capital = "Lincoln"</code>

In the code above, there’s a table named `states` with a subtable for each state, and it sets the value of `capital` for Nebraska to "Lincoln.”

Quit and relaunch the app — it’s still there.

Like dictionaries, tables have no schema. You can put anything you want into any table. And of course scripts have full power to create, edit, and delete tables and not just values (the database is fully scriptable — that’s the point).

#### Scripts

Just as you can refer to database values using dot syntax, a script can call another script the exact same way. In fact, you do that all the time, because the standard library is also stored in the database.

If you call `file.readWholeFile(f)` — which returns the contents of a file as a string, given the path — you’re actually calling a script `readWholeFile` that lives in a table named `file`, which contains the standard library’s file verbs.

And of course that works with your own scripts too. There are no import statements — you just call, using dot syntax, whatever you want to call.

The debugger has the standard things — step into, continue, etc. — and you can view the stack when you debug. The stack is just more tables! Which you can also edit, while you’re debugging, like any other Frontier tables.

And the debugger works across scripts — you can step into a call to another script and continue debugging. (This is super-common, even.)

Your one-off scripts are typically stored in the `workspace` table. For collections of scripts that work together — as a kind of app — you’d create a “suite” (a table containing scripts and data) or, in later years, you’d put them together in a separate “guest” database.

Getting around was super-easy — if you saw `file.readWholeFile` in a script, for instance, you’d cmd-double-click it to jump to that location in the database.

Brilliantly, and I think uniquely, scripts were written in an *outliner*. Scripts are, after all, tree structures — and using an outliner for code folding and reorganizing has huge advantages. It feels surprisingly natural, too. I know how how weird that must sound to anyone who’s never written code that way. But, really, all other code editors seem sad to me in comparison, like reindeer that can’t fly. The outliner spoiled me.

(Tabs vs. spaces was never an issue, at least!)

#### In the end

It was just so easy to start something, and then refine it and keep going, and make things that did useful things.

We wrote blogging software and RSS readers and all kinds of early open web things. (It even had a built-in webserver.) It was fun — it was a *joy*, even.

I think the Mac is missing this app. So my goal with [Rainier](https://github.com/brentsimmons/Rainier) (which is a mess at the moment) is to do a new, modern Mac app inspired by Frontier. It won’t be compatible with Frontier, and lots of details will be different, but I hope to capture that same lightning, which, I think, we could use right now.

I could be wrong! Worst case is that I’ll just get back the fun that I miss so much. Which is okay. :)

PS Somebody somewhere is thinking that this is like a very weird, not-object-oriented Smalltalk. It is! But that doesn’t make it less awesome.

PPS I’ve left out a *ton* of details, but I hope I’ve gotten the gist of this across.

PPPS If you’re interested in joining the Slack group and helping me with my thinking, just email me. (You can find my email on [this page](http://ranchero.com/netnewswire/).)
