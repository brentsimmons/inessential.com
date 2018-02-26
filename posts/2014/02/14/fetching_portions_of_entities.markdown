@title Fetching Portions of Entities
@pubDate 2014-02-14 20:58:42 -0800
@modDate 2014-02-14 20:58:42 -0800
My previous post led to some Twitter traffic, and it led Dad (he goes by Dad) to [do some investigating](http://geekanddad.wordpress.com/2014/02/14/core-data-efficient-fetching-of-portions-of-entities/).

The documentation for setPropertiesToFetch says one thing and the .h file says another. Contrary to the documentation — but per the .h file — you can use this with managed objects. From the .h file: “the results are managed object faults partially pre-populated with the named properties.”

This almost what I want.

What I’d like even more is to get objects back as faults, but have only those specified properties fetched when the objects are un-faulted.

Other properties would get fetched only when one of them is accessed. Which wouldn’t happen in the case of Vesper’s timeline, but would happen when a note’s detail view is displayed.
