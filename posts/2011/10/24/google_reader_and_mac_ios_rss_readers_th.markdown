@title Google Reader and Mac/iOS RSS readers that sync
@pubDate Mon Oct 24 21:38:42 -0700 2011
@modDate Mon Oct 24 21:46:55 -0700 2011
The recent <a href="http://googlereader.blogspot.com/2011/10/upcoming-changes-to-reader-new-look-new.html">announcement of changes coming for Google Reader</a> worries me some. Though I don’t use Google Reader directly, I — like many iPhone, iPad, and Mac users — use RSS readers that sync via Google Reader.

This announcement isn’t just a reminder of the fragility of the system: it removes some features that people use. Google Reader’s social and sharing features are going away in favor of integration with Google+.

This makes sense from Google’s point of view — a single, Google-wide social network should be better than a separate network for each Google app.

Nevertheless, there are users who will miss the current, about-to-disappear features. (See <a href="http://nick.typepad.com/blog/2011/10/what-the-upcoming-google-reader-changes-mean-for-feeddemon.html">What the Upcoming Google Reader Changes Mean for FeedDemon</a> for an example of how one RSS reader will have to change.)

When I say that the system is fragile, I don’t mean that Google Reader itself is fragile. I mean that using it as a syncing system for other apps is fragile. There are a couple things that RSS reader developers know, that the average RSS reader user probably doesn’t know, which will make this more apparent:

1. The Google Reader API is undocumented, unsupported, and unofficial. This is unlike <a href="http://code.google.com/apis/maps/">Google Maps</a> and others which do have documented and official APIs.

2. Because the API is not official, there is no commitment to keeping it working.

Though RSS reader developers have received much-appreciated unofficial support from Google, that’s not the same as building a feature on solid ground. Smart developers are rightly uncomfortable relying on undocumented, unofficial, unsupported APIs.

But, because syncing is so important for so many RSS reader users, developers have had to gamble. With syncing part of the definition of a minimum viable RSS reader, and with Google Reader the only option for syncing, the choice to use Google Reader is more necessity than choice.

<h4>Questions about the future</h4>

The gamble has paid off so far, with the exception of the features about to be replaced. It’s been an especially good thing for RSS reader users, who can mix-and-match clients on different platforms, who can move with relative ease between one client and another. (The situation is similar to Twitter clients: users are not stuck with one client from one particular developer.)

While I remain optimistic about the future of Google Reader and apps that sync via Google Reader, there are a few reasons for concern:

1. Though Google Reader is a mature app, its lack of an official, documented, supported API sends a message, intended or not, about its importance to Google. And Google has cut apps before, even high-profile apps like <a href="http://googlewave.blogspot.com/">Google Wave</a>.

2. FeedDemon author <a href="http://groups.google.com/group/fougrapi/browse_thread/thread/b0eb7f67939c627">Nick Bradbury asked</a> on the unofficial API support list if Google Reader is being retired. At this writing, a couple days after the recent announcement, the question remains unanswered.

3. Despite all the <a href="http://twitter.com/#!/search/googlereader">#googlereader</a> and @googlereader traffic on Twitter since the announcement, the <a href="http://twitter.com/#!/googlereader">@googlereader</a> Twitter account has been silent. (At this writing.)

4. The wording of the recent Google Reader announcement emphasized how users could export their data. While that’s a good thing — being able to move one’s data is important — the emphasis made it seem like a request or a warning. That characterization is mine, yes, but it’s shared by other developers (not just RSS reader developers) that have read that announcement. This may not have been the author’s intention: it’s possible the author was being careful and doing the right thing by mentioning data exporting. But it didn’t read that way, at least to some developers.

5. We don’t know what the value of Google Reader is to Google. It doesn’t appear to have ads a la search or Gmail, though ads do appear in feeds via Google’s AdSense for feeds, and that presumably makes money. Does Google Reader feed the search engine ranking system? Does it exist to help ensure the goodwill of influential writers who use Google Reader? I can speculate, but I don’t know, which is my point.

At any rate, I remain optimistic, because I don’t have any solid reason to expect things to change.

But Google Reader *has* just changed, and some syncing RSS readers will lose some features, and I take that as a reminder that it could change in a way that breaks syncing, and Google would not have broken any official APIs.

I’m not an RSS reader developer any more. But if I were, I’d start looking for an alternative syncing system right now.
