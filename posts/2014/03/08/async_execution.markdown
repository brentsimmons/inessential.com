@title Async Execution
@link http://jaanus.com/blog/2014/03/08/chaining-execution/
@pubDate 2014-03-08 15:49:56 -0800
@modDate 2014-03-08 15:49:56 -0800
Jaanus, <a href="http://jaanus.com/blog/2014/03/08/chaining-execution/">Chaining execution</a>:

>Sometimes I’ve seen these animations chained by timing: the engineer calculates how long each animation takes, and delays the next one by that amount. Not only is this brittle and looks ugly in code, but it may introduce crash bugs, as the context may change during execution: the objects may go away without knowing it themselves, and happily try to run animation when it’s no longer valid to do so.

>The solution to both of these things is to use block-based APIs.
