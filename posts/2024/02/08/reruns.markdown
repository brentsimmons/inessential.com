@title Reruns
@pubDate 2024-02-08 08:16:00 -0800
@modDate 2024-02-08 08:22:22 -0800
It’s not a bug in your RSS reader if recent articles in this feed all suddenly appeared as unread. You may even have seeming duplicates.

Sorry about that! It’s due to my changing settings in my blog generator. Pages now have a .html suffix where before they had none. This change impacts permalinks, which also changes the `guid`s in my RSS feed — and NetNewsWire and other RSS readers use the `guid` property to identify articles, which means these will show up as new articles.

(Note: I’ve created redirects so that old links pointing in will still work.)
