@title Mocks, Progress
@pubDate 2014-03-12 21:00:29 -0700
@modDate 2014-03-12 21:00:29 -0700
A couple interesting links:

Graham Lee discusses OCMockObjects in [Making a mockery with Mock Objects](http://blog.bignerdranch.com/4668-making-mockery-mock-objects/) on the Big Nerd Ranch Blog:

>In this scenario, the mock object is acting like a VCR, but without the chunky 1980s styling and the mangled ribbons of tape. During your test, the mock records every message you sent to it. Then you ask it to play that back, and compare it with the list of messages you wanted to send. Just like with a VCR, if you were expecting *Gremlins 2* but actually recorded the news and the first half of an episode of *Cheers*, that’s a disappointing failure.

Ole Begemann explains [NSProgress](http://oleb.net/blog/2014/03/nsprogress/):

>Apple is setting a new standard here that will hopefully be widely adopted by the open-source community. If you write code that would potentially benefit from reporting progress of the work it does, you should strongly consider adding support for `NSProgress`. As we will see, you wonʼt have to modify your codeʼs public API to do that. In most cases, it is enough to add just a few lines of code to the method that performs the actual work. By using an established standard, you will make your code easier to use for other developers and easier to integrate with other components.
