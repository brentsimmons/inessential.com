@title Some details about NetNewsWire Lite 4.0
@categoryArray NetNewsWire
@pubDate Wed Mar 02 22:41:07 -0800 2011
@modDate Wed Mar 02 22:42:15 -0800 2011
Some of the particulars, in no particular order...

<h4>It requires 64-bit processors</h4>

This is because when Flash crashes on 32-bit machines, it takes down the app with it. When Flash crashes on a 64-bit machine, it’s just Flash that crashes.

<h4>It doesn’t have syncing, starred items, AppleScript support, searching...</h4>

This really is a <em>Lite</em> version, by design. Like NetNewsWire Lite used to be — just the basics.

I’ve been using it for a couple months as my everyday news reader. Beta testers have had it almost as long. And while I’d like to have syncing, searching, starred items and so on, I’ve been really happy with its <em>speed</em>. And I love the little thumbnails. That mark-all-as-read is finally undoable.

That you can set the refresh time to 10 minutes. That it supports gestures. That you can edit feed names inline. That it launches and quits very fast.

<h4>Folders</h4>

Though there are no folders by default, you can create one via File > New Folder.

<h4>Non-synced feed advantages</h4>

There are a couple advantages to non-synced feeds. The first is that it can read authenticated feeds, which Google Reader doesn’t support. Another is that the news comes in faster — you don’t have to wait for Google Reader to get it beforehand.

(But I know, yes, that syncing is important, and it’s totally planned for the full version of NetNewsWire 4.0.)

(And you can run this alongside an older version of NetNewsWire or any other reader — it’s a separate app.)

<h4>Customize toolbar has a bunch of commands</h4>

Everything that appears in the Share menu can also appear as single buttons in the toolbar. Choose View > Customize Toolbar.

<h4>Forum, bugs/feature requests, Help book</h4>

There’s a new <a href="http://groups.google.com/group/nnwmac-lite">forum</a> (a Google Group) for the app, and a new <a href="https://nnwlitemac.uservoice.com/">UserVoice</a> site for bug reports and feature requests. There’s a <a href="http://ranchero.com/help/netnewswirelite4/">Help book</a> too. All of this is in the Help menu (you don’t have to bookmark this page or any of those links).

<h4>Notes for developers</h4>

It uses Core Data — even though I’ve <a href="http://inessential.com/2010/02/26/on_switching_away_from_core_data">written previously</a> about the drawbacks. (I’ll do a follow-up post.)

The article list is a custom NSScrollView — I wanted a table view with views, something like UITableView. It’s not hard to write. (But, on the other hand, I’m not actually suggesting you do that.)

