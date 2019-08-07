@title Feed Discovery with Feed Compass
@pubDate 2019-03-11 13:07:24 -0700
@modDate 2019-03-11 13:07:24 -0700
Maurice Parker, who’s contributed a lot to NetNewsWire, has started working on a directory app for feeds: [Feed Compass](https://github.com/vincode-io/FeedCompass).

It’s still at the proof-of-concept phase — very early days. The idea is that it can read OPML files from the web, show you a list of feeds, and show a preview of what’s in a feed when you select one. Most importantly, there’s a big Subscribe button so you can add the feed to your RSS reader.

The subscribe button should work with any Mac RSS reader that supports the `feed` protocol (which is probably all of them). It’s not just NetNewsWire-specific, in other words — it should work with [Reeder](http://reederapp.com/mac/), [ReadKit](https://readkitapp.com/), and others. (I haven’t tested this, though.)

<p style="text-align:center">* * *</p>

This isn’t *all* of what needs to be done to make feed discovery easier and better. It’s a step, though, and it can be combined with other steps.

Some things I like about it:

* It’s decentralized. It doesn’t rely on any one server, since servers may come and go.
* It’s open source, which means you can contribute and/or fork. The code can’t go away.
* It’s free, which means there’s no barrier to use.
* It works (as I mentioned) with any Mac RSS reader, not any one in particular.
* It could be ported to iOS.
* It means we don’t need to include a feed directory built-in to NetNewsWire. (This helps keep NetNewsWire focused.)

<p style="text-align:center">* * *</p>

Again, this is just the start of something. It’s not the one and only true answer to the problem of feed discovery — but it could be part of a collection of solutions that work together.

For more about discovery… When Maurice was doing research on the topic, he found [this thread](https://github.com/scripting/Scripting-News/issues/96) on Dave Winer’s GitHub enlightening, and I recommend reading it.

<p style="text-align:center">* * *</p>

I had posted, to the NetNewsWire Slack group (email me for an invitation), a list of RSS app ideas. These are apps that could use NetNewsWire code to get a head start (though you wouldn’t have to).

The below is what I posted…

Here are some ideas for apps I’d love to write, that could use some NetNewsWire code, but that I’m too busy to write — but that would be cool if someone else wrote!

**Big Internet Backup** — discussed earlier. Give it a bunch of feeds, and it keeps everything forver. Searchable. Smart feeds. Etc.

**Timeline/river-of-news reader** - RSS presented as in a Twitter client. Reverse-chronological list. Super simple. Probably doesn’t even track read/unread (just position in timeline).

**Microblog client as productivity app** — multiple accounts, standard sidebar. Features like drafts. Scriptable. Searchable. Keeps items for a long time. Possibly even a detail pane that shows linked-to web pages. Connection to MarsEdit.

**Feed creator** — makes it easy to create feeds, including podcast and appcast feeds. (For instance: I do the appcast feed for NetNewsWire _by hand_, which is crazy. There should be an app for this.)

**Feed debugger** - given a feed, this app tells you about the issues. Is it a valid feed? Does it support conditional GET? Are attributes missing? Misspelled? Etc. This is especially important as it appears that feedvalidator.org may be down for the count.

**Feed directory** - reads in OPML from various sources on the web (such as Dave Verwer’s and Dave Winer’s collections) and creates a directory. When you select a feed, it downloads it and shows a preview of what you’d get. One-click subscribe to the default reader (whether it’s NetNewsWire or another app).

Though ideally these would be open source apps, they don’t have to be. (You can use NetNewsWire code in commercial apps, as long as you credit NetNewsWire in the about box or somewhere appropriate.)

I don’t claim that any of these are money-makers. Maybe some of them? Depends. I do think they’d all be very useful, and that you have a leg up since you can start with NetNewsWire code.
