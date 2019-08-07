@pubDate 2019-06-09 20:37:53 -0700
@modDate 2019-06-09 20:37:53 -0700
Catalina compatibility tip: don’t use NSFont as a key in a Swift dictionary. I’m getting crashes from 10.15 users that include this message:

> Fatal error: Duplicate keys of type 'NSFont' were found in a Dictionary. This usually means either that the type violates Hashable's requirements, or that members of such a dictionary were mutated after insertion.

It’s quite possible this was always a bad idea, of course, and it’s just that in 10.15 it crashes. I don’t know.
