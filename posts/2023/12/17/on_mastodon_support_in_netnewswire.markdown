@title On Mastodon Support in NetNewsWire
@pubDate 2023-12-17 18:56:35 -0800
@modDate 2023-12-17 19:07:50 -0800
Tim Chambers, admin of the Mastodon server indieweb.social, which hosts my personal account and the NetNewsWire account, <a href="https://indieweb.social/@tchambers/111596493325633510">asked me</a> if ActivityPub support is on the roadmap for NetNewsWire. Great question!

Tim was responding to <a href="https://mastodon.social/@ricmac/111596432765792578">Richard MacManus</a>:

> Are there any RSS Readers that are trying to integrate ActivityPub too? Pondering the glut of email newsletters in our inboxes these days, and wondering if we are due for an RSS Reader renaissance, except with a fediverse twist this time…

I hear this. It’s not the first time this has come up, and I’ve spent the past year or so thinking about it.

Since RSS is an open web thing that brings you stuff people write, and ActivityPub is also an open web thing that brings you stuff people write, it’s an obvious good idea to do both in the same app. Totally.

But the question was specifically about NetNewsWire.

We will make NetNewsWire work better with Mastodon-generated RSS feeds. There are some things we’re not doing yet that will make reading these a better experience.

But should NetNewsWire become a Mastodon client? That’s where the answer is not so obvious.

<p align=center>* * *</p>

Let’s compare the NetNewsWire and Mastodon experiences.

NetNewsWire is a three-paned RSS reader. Sidebar (accounts, folders, feeds) on the left. Timeline (titles and/or first few lines) in the middle. Article on the right. [See these screenshots](https://netnewswire.com/screenshots.html) to get the idea.

Each article has a read/unread status. Selecting an article marks it as read, and there are commands to mark all as read (and mark all as read above or below the selection).

This is not the only good model for an RSS reader, but it’s how NetNewsWire works — and it’s a bad fit for a Mastodon reading experience.

Whether you use Mastodon on the web or in an app you’re used to a single timeline per account (with perhaps side streams for mentions and such). All posts from everyone you follow appear in that single timeline. You don’t deal with read/unread status — instead you have a chronological position.

The timeline shows the entire post (usually), instead of an optional title and first few lines. There is no third article view, because the entire post is displayed in the timeline.

This experience isn’t unique to Mastodon, of course — that’s how X, Threads, Micro.blog, Bluesky, and other social media apps work.

But it’s not how NetNewsWire works, and if we try to mash that experience into the app — but have it on only when a Mastodon account is selected — we’d end up with a confusion that feels like two very different apps. Because it would be.

<p align=center>* * *</p>

A second option: we could not change the experience and just assume that some people would like to use Mastodon in a NetNewsWire way instead of in the usual social media way. I’m extremely skeptical of this idea — I think it would be a pain, and I think most people who try it would drop it.

The third option, which I think is best, which we already do, is to support Mastodon via RSS. (Mastodon feeds are usually available as RSS — you can add `.rss` to the end of a URL to get a feed.)

There might be some Mastodon accounts you want to follow in your RSS reader instead of in your Mastodon client. Think of an account for a website that doesn’t have an RSS feed, but that reliably posts links to articles. Or a person you want to follow — but you don’t want to show up in their follower list. (Sounds a little antisocial, sure, but you can imagine good reasons.)

We can, and will, do more to make Mastodon-over-RSS a good experience in NetNewsWire. Right now we’re not picking up avatars or image attachments, which we can fix. There might be more things like that to do. We might add the ability to post to Mastodon, since it’s a natural thing to want to share stuff from your RSS reader to Mastodon.

But I don’t think we’ll make NetNewsWire a real Mastodon client.

<p align=center>* * *</p>

It still seems like RSS and Mastodon could fit in the same app, though! If I were designing it, I’d start with the social media experience: the single timeline of posts. Very simple sidebar. No article view. No read/unread status — just position in the timeline.

You could add RSS feeds, but they’d be treated like Mastodon posts. Any article short enough would appear in full in the timeline, but most would probably have to be truncated. You’d open articles in your browser, just like you do now with social media apps (there’d be no third article pane).

Such an app could be a nice unified experience. Get your Mastodon, Threads, RSS feeds, Micro.blog and, hopefully, other services — anything that supports ActivityPub, RSS, or some other open format or API — all in one place, in a way that’s already familiar to everyone.

Sounds pretty great! But it’s not NetNewsWire.
