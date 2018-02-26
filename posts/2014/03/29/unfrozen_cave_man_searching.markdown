@title Unfrozen Cave Man Searching
@pubDate 2014-03-29 17:01:47 -0700
@modDate 2014-03-29 17:23:02 -0700
I didn’t like how searching was implemented in Vesper 1.x. I’ll describe it so you can freak out at me. I’ll note that it does have the advantage of working, but that’s it.

#### Vesper 1.x Searching

Given a search string, it queries the database with one or more `like %word%` expressions. (One for each word in the search string.)

The database has a `searchText` column that is a copy of the `text` column but with everything made lower-case, with whitespace and punctuation removed, and with diacritics stripped.

In other words, if note.text is “Pick up some milk and éclairs” then note.searchText is “pickupsomemilkandeclairs.”

While this works, it’s not pretty. It means keeping that `searchText` column updated, and it means a larger database than I’d want. It means repeating data which is very not cool — that’s where it feels the ickiest.

#### What I Should Do

SQLite has [full-text search (FTS) extensions](https://www.sqlite.org/fts3.html). (I believe these are included with the on-the-system SQLite. If not, I’d have to compile my own SQLite and use that. Do-able.)

While I’d like to use FTS, it’s more of an effort than is warranted at the moment. (My priority is syncing.) In particular I’d have to determine if it supports character sets such as Chinese and Japanese. A little research leads me to think that my only option is writing some code and testing, which is more than I’m going to do right now.

(I *will* get to this, but not now.)

So that leaves me with my old-fashioned approach. One day a few months ago I nuked that `searchText` column in the database, which means that searching has been broken in the dev version of Vesper for a while. Any solution needs to not use that column.

#### What I Did

Conceptually I’m still doing the same thing: checking each note to see if it contains all the words in the search string. I’m still lower-casing and still stripping whitespace and diacriticals. (But leaving punctuation in place, at least at the moment, which is a difference.)

The difference is that I’m doing this on-the-fly, by adding a custom function to SQLite, which is something I’d not done before, which turned out to by easy. Here’s a [gist from Gus](https://gist.github.com/ccgus/3238464) which shows how it’s done.

This is cool because I can write a query like <code>select blah where textMatchesSearchString(text, ?);</code> — where textMatchesSearchString is my own code.

And textMatchesSearchString is simple. It uses `enumerateSubstringsInRange` to loop over the search words, then uses `rangeOfString` with `NSCaseInsensitiveSearch` and `NSDiacriticInsensitiveSearch` to check for matches. If a row’s text matches all search words, then it returns YES via `sqlite3_result_int`. (It’s a custom SQLite function, sure — but it’s just a block, and Objective-C and Cocoa are perfectly legal in that context. Nothing weird.)

It’s still plenty fast enough. I don’t even notice the fetch time. And that evil `searchText` column remains gone.

#### Future

The longer Vesper exists, the more likely are big databases. This solution won’t be good enough forever — I’ll have to start using some kind of full-text search eventually. (Probably SQLite FTS, though I can’t say for sure.)

I hear the siren call, loud and lovely, enticing me to go all the way to FTS *right now*. But I resist, knowing that delays to shipping syncing just aren’t worth it. Somehow I resist.

(You’re still welcome to freak out at me.)
