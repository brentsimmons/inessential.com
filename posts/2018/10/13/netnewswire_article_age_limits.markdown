@title NetNewsWire Article Age Limits
@pubDate 2018-10-13 14:41:05 -0700
@modDate 2018-10-13 14:41:05 -0700
RSS readers — at least the several where I know how they work — have some limits on how long they keep articles and how long they track read/unread status.

I may not have the details exactly right, but I recall that Google Reader stopped tracking read/unread status for every article older than 30 days. With NewsGator it was two weeks or the most recent 200 articles. Older versions of NetNewsWire had different limits, depending on which version you’re talking about.

There are several good reasons for limits. One is ethical: piling up unread articles forever isn’t fair to people. Your RSS reader should not be a taskmaster or a source of guilt. Articles should age out after a period of time.

Another is that the more data is saved, the slower database lookups tend to get, and the slower the app gets. In the case of a Mac or iOS app, this also means using more disk space and more energy (more battery).

A third is that if an RSS reader sets the expectation that it creates a personal backup of the internet, then the developer will be doing features, bug fixes, and performance optimizations for this forever, to the detriment of the rest of the app and the majority of its users. (I went through this with earlier versions of NetNewsWire.)

Limits are a necessity. The hard part is deciding what the limits should be, and figuring out how to make them understandable to users.

NetNewsWire will sync with various systems ([Feedbin](https://feedbin.com/) and similar), and, for each syncing account, it will just adopt the limits of each system.

But that still leaves one case where the limits need to be worked out: the non-synced On My Mac account. The below is my thinking (after much discussion with other people) on this.

#### The Rule

Articles older than n days will be deleted automatically — but it will preserve a minimum of the 10 most recent articles per feed, and it won’t delete starred items.

(Where n is something like 90 days.)

This is slightly more complex than just aging out older articles. It makes sure that feeds that haven’t been updated in a long time still have their most recent 10 articles.

I think this is reasonable because you don’t want to click on a feed and see zero articles just because it hasn’t been updated in six months (or whatever).

But there’s a tricky part here: how do we define the age of an article? Seems like it should be obvious, but it’s not.

#### Publication Date vs. Arrival Date

Every article has three dates, though two of them may be empty.

* Publication date: the date specified in the feed when the article was published (may not exist in the feed)
* Modification date: the date specified in the feed when the article was edited (may not exist in the feed)
* Arrival date: the date NetNewsWire first saw the article (guaranteed to exist, since it’s NetNewsWire-generated)

Most of the time, arrival date and publication date will be pretty close. Not always, though — not, for instance, when adding a feed. When it reads a feed for the first time, the arrival date is that moment for each item, while the publication date could be anything.

You might think, naturally, that NetNewsWire should use arrival date when deciding whether or not to delete an article. If it *arrived* more than n days ago, then it should be deleted, because that means the user has had it for more than n days.

But there’s a problem with that: arrival date is never shown in the user interface. It’s not otherwise an interesting piece of information, where publication date *is* interesting to users.

So if we have a time-based limit that’s triggered by unseen metadata (arrival date) — and there is *visible* metadata (publication date) of the exact same type and that seems like it’s directly relevant to age — then I think we have to use the *visible* date, the publication date.

This makes the limit understandable: you can see the dates, after all, that it uses for its calculation.

(Note: when publication date isn’t specified in the feed, then NetNewsWire uses the arrival date as the publication date, since it will usually be pretty close. Luckily, feeds do tend to include publication dates.)

The one drawback to using publication date, though: it could delete an article with a recent arrival date but a long-ago publication date. I think this is okay — I think it’s the best of the available trade-offs.

#### The Other Tricky Part: Communicating with the User

The app shouldn’t behave mysteriously. How this works should be clearly communicated.

One option is to just to write about it in the Help book. Unfortunately, people don’t read these all that much.

So here’s what I’m thinking:

Since there will be a preference pane where you can add and edit your various sync accounts (much like in Mail), we have a place for settings for the On My Mac account.

In those settings would be something like this:

<code>Delete articles published more than: [popup] 30 days ago / 90 days ago / 120 days ago</code>

With explanotext:

<code>The On My Mac account deletes older articles when there are more than 10 articles in a feed. It never deletes starred articles.</code>

Though I most definitely like to limit preferences, this is a reasonable thing to want to configure — and having this there makes it much more likely that a user will see it and learn about the limit.

I think that’s the best call, though it’s not set in stone yet.

#### Reminder: None of This Applies to Syncing

After reading all these words, you might have forgetten that I’m just talking about the limits of the On My Mac account. Different syncing systems have their own limits, and NetNewsWire will adopt those for the synced accounts.

#### Feedback welcome

If you go to the [repo](https://github.com/brentsimmons/NetNewsWire) you can find my email address and find the bug tracker. You can always email me to ask to be added to the Slack group. But — fair warning! — a lot of the discussion is over super-dry stuff like this issue.
