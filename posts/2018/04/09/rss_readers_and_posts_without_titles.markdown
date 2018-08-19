@title RSS Readers and Posts Without Titles
@pubDate 2018-04-09 13:02:41 -0700
@modDate 2018-04-09 13:08:32 -0700
I’m quite aware that my recent blog posts without titles look weird in some RSS readers.

Here’s the thing, though: the RSS `title` attribute was always optional. It’s just that RSS readers were written with the expectation that it was mandatory.

If you write an RSS reader with a timeline and detail view, here’s what you could do:

* Use the first part of the `description` in the timeline, after stripping HTML.
* Show the post in its entirety in the detail view — but minus a title. No “Untitled,” no synthesized title. Just no title at all.

If you want to see an example, subscribe to this blog in [Evergreen](https://ranchero.com/evergreen/). Sure, it’s not 1.0 (or even beta) yet, but it handles title-less posts the way I’ve described above.

#### It’s the future

Here’s why this is important:

We’re already seeing more and more microblogs, and we’re seeing blogs like this one that have some long posts and some microblog posts. (When you see the word “microblog,” think tweet-like, but with HTML.)

This is an important part of the future of blogging. It’s the movement away from posting to Twitter first — instead, you post to your blog (or microblog) and then, optionally, echo the post to Twitter.
