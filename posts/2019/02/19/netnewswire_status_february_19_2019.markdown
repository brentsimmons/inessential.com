@title NetNewsWire Status: February 19, 2019
@pubDate 2019-02-19 13:35:45 -0800
@modDate 2019-02-19 13:35:45 -0800
There are three big things that [remain](https://github.com/brentsimmons/NetNewsWire/milestone/1) before the first feature-complete build (which will be 5.0a1): searching, the app icon, and syncing with FeedBin.

Brad Ellis is working on the app icon, so that leaves searching and syncing (and a few miscellaneous bugs) for me.

I’ve been working on searching — I want to get that done next, and then do syncing as the last thing before hitting alpha 1.

#### How search is implemented

The UI for searching is pretty straightforward: you type into the search field, and then the timeline shows your search results. Click on an article to show it in the detail web view. Exactly as expected.

But there are two ways I can think of to implement this UI.

1. When a search starts, do the search and show the results in the timeline. When the user ends searching, restore the previous timeline and detail view states.
2. When a search starts, swap in a separate timeline and detail view, do the search, and then show the results in these swapped-in views. When the user ends searching, swap those views out, and swap back in the regular timeline and detail views.

Ideally the user can’t tell the difference between the two methods. But if you go with solution #1 — use the existing timeline and detail views — then you have the challenge of restoring state, including selection and scroll positions, when searching ends.

If you use solution #2 — swapping views in and out — then you don’t have that challenge. State is restored exactly as it was, because you saved the non-search views and swapped them back in.

(If you look at other apps — Mail, for example — it appears they use solution #1, and state restoration is not always instant. I want it to be instant.)

So, for the past week, I’ve been re-jiggering so that I can have multiple timeline and detail views and swap them in and out.

(This is not that different from how searching in iOS apps is supposed to work.)

And then, last night, as I finished the re-jiggering, I did the actual search-in-the-database implementation, which took about an hour.

This still leaves me to handle changes to the search field, so that the search is actually run at the right time, and so that searching ends properly. I expect that to take a few hours to get all right. (I’ve done this before, and it’s always slightly more complex than it seems.)

#### Why do I make this point?

If you’re not a programmer — or you’re new to programming, or haven’t written apps with a user interface — it’s easy to think that the actual under-the-hood implementation of a feature is what takes the most time.

It’s not. In the case of the search feature, I spent more time just *thinking* about how I want to do the UI than on the actual search-in-the-database implementation. And then there’s the UI work itself, which absolutely dwarfs the database work.

Another case: you might imagine that the bulk of the work in NetNewsWire was writing an RSS parser, for instance. But no. While that code is critical, obviously, it’s very, very small compared to the user interface.

And, similarly, the part of syncing that’s just making API calls and updating the database will be the easy part. The part that takes longest will be user interface. A factor of ten would not be surprising.
