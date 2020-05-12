@title More on the Default Feeds Issue
@pubDate 2020-05-11 18:08:44 -0700
@modDate 2020-05-11 18:20:16 -0700
Here’s the latest on the [story from yesterday](https://inessential.com/2020/05/10/heads_up_to_rss_reader_authors).

NetNewsWire 5.0.1 for iOS was approved for the App Store this morning, and I assumed that was the end of it. I figured this whole thing was just an error.

But later today I heard from Apple that, while this latest version has been approved, the app is now under further review for this issue.

This isn’t quite over yet — but at least we could ship 5.0.1, so that’s cool, and I’m glad.

#### More Details

The issue really is about the default feeds. They’re added by default on the first run of the app.

Apple suggested some options — things I could do if, after further review, they decide that I need to bring the app into legal compliance:

* Provide documentation (to Apple) expressing permission to use those feeds as defaults
* Have the user, on first run, pick from a list of these feeds
* For these feeds, show only a title, and then link out to Safari

For now I’m not doing any of those things, since Apple’s review is ongoing. I’ll wait for the review to complete.

If the review completes and I _do_ need to do something, I’ll take the first option: I’ll get the necessary documentation.

(Yes, I could change the UX instead. But I don’t want to — the app works the way I think is best. You could debate whether I’m right or wrong on that point, but there’s no debating that this is the UX I want.)

#### I’m Not Actually Against Getting Permission

As I wrote on the [NetNewsWire FAQ](https://ranchero.com/netnewswire/frequently-asked-questions) about the default feeds:

> We change the feeds from time to time. We don’t have any arrangements with the feed owners, though we usually ask permission — unless it’s something like Daring Fireball or Six Colors where it would obviously be no problem.

The authors of Daring Fireball, Six Colors, and a few other sites are friends, and I don’t need to bug them to ask permission. There are other default feeds where I know the people less well (or not at all), and I have asked permission from people — not because I was worried legally but because it seemed like basic courtesy. I don’t think anyone’s ever said no, but I did want to give them the chance.

But can I find all these conversations, and can I turn those conversations over to Apple without asking the other parties?

I don’t think so. So this would mean going through and getting explicit permission from a dozen-ish different people and turning copies over to Apple.

Which is fine. I can do that if Apple decides they need that documentation. It’s not onerous.

#### What Still Rubs Me the Wrong Way

I’m trying to figure out what bothers me. I think there are two things.

One is just that the App Store has always seemed rather arbitrary. The guidelines don’t even have to change for unseen policies to change, and it’s impossible to know in advance if a thing you’re doing will be okay and _stay_ okay. (Recall that NetNewsWire has been doing the same thing with default feeds for 18 years.)

This gets really tiring, because every time we submit an app — even just a bug-fix release, like 5.0.1 is — I have to deal with the anxiety as I wonder what’s going to happen this time.

The other issue is a little harder to explain, but it goes like this:

If a site provides a public feed, it’s reasonable to assume that RSS readers might include that feed in some kind of discovery mechanism — they might even include it as a default. This is the public, open web, after all.

Now, if NetNewsWire were presenting itself as the official app version of Daring Fireball, for instance, then that would be dishonest. But it’s not, and that’s quite clear.

To nevertheless require documentation here is for Apple to use overly-fussy legal concerns in order to infantilize an app developer who can, and does, and rather would, take care of these things himself.

In other words: _lay off_, I want to say. I’m an adult with good judgment and I’ve already dealt with this issue, and it’s mine to deal with.
