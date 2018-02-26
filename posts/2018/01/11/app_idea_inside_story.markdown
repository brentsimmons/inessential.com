@title App Idea: Inside Story
@pubDate 2018-01-11 13:09:35 -0800
@modDate 2018-01-11 13:09:35 -0800
I had this idea around the time Apple came out with Bonjour (née Rendezvous), and all these years later I realize I’m never going to get around to it.

Here’s the scoop:

The idea is microblog posts (tweet-like) but that live inside a specific network only.

You run a Mac app that:

* Lets you post short messages.
* Shows short messages from people inside your network.

The app runs a small webserver that’s discoverable via Bonjour, that has a specific service name. That webserver publishes a feed of your posts.

The app also downloads a feed from every other app it finds (and caches those feeds, for when other apps are offline).

In other words, it’s instant office microblogging with no centralized server. Completely peer-to-peer.

The design is what you expect — a reverse-chronological list of posts with usernames and avatars. You can reply, mention people, mute people, etc. (I think you’d follow everybody on the network automatically — so muting becomes the thing, not following.)

<p style="text-align:center">* * *</p>

Important thing: your posts are network-specific. So if you go to a coffee shop or the airport with your Mac, you won’t be publishing your at-the-office posts.

<p style="text-align:center">* * *</p>

I haven’t done research into whether this is do-able on iOS. Is it possible to run a little webserver, in a backgrounded app, that other people on the local network could connect to? Seems unlikely — but I don’t know. Cool if you could.

<p style="text-align:center">* * *</p>

I have no idea how you’d make money with this one. If you charge for it, not enough people would use it to make it worthwhile. (The standard dilemma of social networking apps.)

Maybe, though, you could add some IAP features? One might be to let people add RSS feeds, so it could also function as a lightweight RSS reader. A person might want posts from Daring Fireball and wherever else added to their timeline.

Or just add that feature anyway, and do the whole thing for fun.

PS “Inside Story” is a long name. Should be one word. Scoops? Bulletins? Officecast? Gossip? (“Gossip” was, if memory serves, the name of an app [Chuck Shotton](https://twitter.com/cshotton) was working on a long time ago. Probably reusable at this point.)

(I mean, c’mon, office Gossip. It’s so perfect.)
