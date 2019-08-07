@title More Thoughts at Random on Blog Search Engines
@pubDate 2019-04-14 11:54:10 -0700
@modDate 2019-04-14 11:58:00 -0700
I can dream about how I’d build one of these. (I’m not going to! This is way outside my expertise, and I have [other things to do](https://github.com/brentsimmons/NetNewsWire).)

Instead of having it crawl blogs, I’d have it download and index RSS feeds. This should be cheaper than crawling pages, and it ensures that it skips indexing page junk (navigation and so on).

To get feeds into the system, I’d add an accounts system to the site. A registered user can do two things: 1) add individual feeds and 2) upload an OPML file of feeds (which they’d probably get from their RSS reader). 

Registration (with an email confirmation loop) would be required for feed-suggesting.

And: a feed gets added to the crawl-and-index list once it’s been suggested by at least *two* users. This should help cut down on spam.

Accounts that are suggesting spam would be just shut down. And suggestion counts for all the feeds they suggested would be appropriately decremented. (And of course all spam feeds should be removed from the index.)

There would also have to be a way for users to report spam. And report hate speech and other things that shouldn’t be there.

<p style="text-align:center">* * *</p>

Anybody should be allowed to use the system: it doesn’t require registration. The main page is like Google or DuckDuckGo — a big search field.

Registered accounts can login and see their saved searches.

Searches should be able to look for incoming links to a given site as well as search terms.

It should also provide search results via RSS — to all people, registered or not — via an easily-constructed URL, as in https://blogsearch.example.com/search.rss?q=some+search+term

Since a search results feed includes items from different feeds, it should use the [RSS source element](https://cyber.harvard.edu/rss/rss.html#ltsourcegtSubelementOfLtitemgt).

<p style="text-align:center">* * *</p>

I don’t have any solid ideas about making this a business. I’m sure that it would be way easier to build than the search engines we had in 2005. And it should be way cheaper to maintain.

It could display ads on the website. Maybe it would offer a subscription that gets rid of the ads and perhaps offers some kind of extra features.

Years ago you could probably get VC funding for something like this. I consider it a blessing that we’re way past VC interest in RSS and blogs — you don’t need that amount of funding to get it built and running, and you wouldn’t want it anyway.

Could a person or small team run it as a labor of love, like I do with NetNewsWire? I’m not sure, because I don’t know enough about the costs involved (other than that they’ve gone down). Maybe?

One of the key would be to keep it simple. It’s just one component in an ecosystem of tools. Do search, and do it well, and that’s it.
