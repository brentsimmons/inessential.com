@title Emptiness
@pubDate Sat Jul 28 12:13:19 -0700 2012
@modDate Sat Jul 28 12:18:49 -0700 2012
I usually don’t care about the differences between nil, null, and just plain empty data — it amounts to the same thing. RSIsEmpty works on NSString, NSArray, NSSet, NSDictionary, and NSData.

RSStringIsEmpty is just an optimization for when I know for sure it’s a string.

<script src="https://gist.github.com/3194441.js?file=EmptyChecks.m"></script>

Hardly earth-shattering code — but useful, and I use these all the time.
