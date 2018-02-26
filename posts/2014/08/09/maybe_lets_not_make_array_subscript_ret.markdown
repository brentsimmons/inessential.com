@title Maybe Let’s Not Make Array Subscript Return an Optional
@pubDate 2014-08-09 15:02:15 -0700
@modDate 2014-08-09 15:02:15 -0700
<a href="http://airspeedvelocity.net/2014/08/08/the-case-against-making-array-subscript-optional/">Airspeed Velocity</a>:

>…developers would probably start to get unwrap fatigue. They inspect the code, see that there’s no way the index could not be valid (there’s no index arithmetic going on there, just use of an index that is guaranteed to be within bounds), and just force unwrap instead.

>This is a slippery slope. Once you start doing that, you do it all the time.
