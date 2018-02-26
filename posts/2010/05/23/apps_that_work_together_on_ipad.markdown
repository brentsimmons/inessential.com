@title Apps that work together — on iPad
@pubDate Sun May 23 20:59:54 -0700 2010
@modDate Sun May 23 21:00:39 -0700 2010
On Macs we have a long-standing culture of apps working together. I can think of a few examples from my own Mac app: you can send a podcast to iTunes, send an article to Twitterrific to tweet it, or send an article to MarsEdit to post it to your weblog.

Of course, on a Mac, the calling app doesn’t quit when you do these things. It stays open. You can get right back to it. (In some cases, the calling app stays in front the whole time, like when sending a podcast from NetNewsWire to iTunes.)

On the iPad (and iPhone) we can sort-of do the same thing. We don’t have AppleScript or Apple events, but we do have the URL scheme thing for inter-application communication. It’s technically possible to do some of these same things.

But we don’t have an easy way to get back to the calling app. Imagine a hypothetical case like this:

1. You’re in Twitterrific, looking at a web page, and there’s a link to a feed. You want to subscribe to that feed.

2. So you choose a “Subscribe in NetNewsWire” command. It opens NetNewsWire and subscribes to the feed.

3. Now that you’ve done that, you want to get back to your place in Twitterrific. You want it to be exactly as if it never quit.

We can do #1 and #2. It’s #3 that’s tricky.

So I have an idea. It just came to me, so I don’t know if it’s good or bad — but it’s worth posting, at least.

What if the calling app added, as a parameter to the URL, a URL to call when the task is completed?

This way the helper app (NetNewsWire in this case) would know, once the task is complete, how to get the user back to their place in the calling app (Twitterrific in this case).

The helper app wouldn’t even have to know anything about the calling app — it’s opening the URL that it was handed. (Maybe there’d be a spot for a success/fail return code of some kind too, but that’s a small side issue.)

Sensible? Silly?
