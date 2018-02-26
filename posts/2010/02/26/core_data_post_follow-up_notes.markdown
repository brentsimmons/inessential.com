@title Core Data post follow-up notes
@pubDate Fri Feb 26 17:30:38 -0800 2010
@modDate Fri Feb 26 17:48:28 -0800 2010
(This is a follow-up to the <a href="http://inessential.com/2010/02/26/on_switching_away_from_core_data">previous post</a>.)

I like <a href="http://rentzsch.tumblr.com/post/414252963/brent-switching-away-from-core-data">Wolf’s NSManagedObjectOperation idea</a>.

I’m checking out Aaron Hillegass’s <a href="http://github.com/hillegass/BNRPersistence">BNRPersistence</a>. I ran across <a href="http://1978th.net/tokyocabinet/">Tokyo Cabinet</a> a couple months ago when building mutt, and it sounded pretty cool, though I didn’t try it any projects.

<a href="http://twitter.com/justin/status/9705599799">Justin asked me</a> if it was worth doing this optimization for the extreme case — 10,000 unread items on a first-generation iPod Touch. It’s not always worth optimizing for extreme cases, not at the expense of other things. But there are several reasons why it was right this time:

- High unread-items-count isn’t the only cause of performance degradation.

- Lots of people still have original iPhones and iPods Touch.

- The performance difference is significant even in a more typical case, say 1,000 unread on an iPhone 3GS.

- The performance difference allows me to do other things that people are asking for.

<i>Update 5:45 pm</i>: I just looked, and the Tokyo Cabinet license is LGPL. Even with the leading L that means I can’t use it, because I don’t want to be a legal test case. (If it came pre-installed on Macs and iPhones, I would feel okay about using it.)
