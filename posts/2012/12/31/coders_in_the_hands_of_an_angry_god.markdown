@title Coders in the Hands of an Angry God
@pubDate Mon Dec 31 09:53:42 -0800 2012
@modDate Mon Dec 31 09:54:53 -0800 2012
Ash Furrow in <a href="http://ashfurrow.com/blog/seven-deadly-sins-of-modern-objective-c">Seven Deadly Sins of Modern Objective-C</a> makes good points. I especially like his reminder to use NSInteger and friends:

>Yeah, that’s right: every time I need a integer in Objective-C, I use NSInteger. If I need it to be unsigned, I use NSUInteger. Every. Time. Same with float and CGFloat. That takes care of the 32/64-bit conversion for me.

The one of his sins that I’m guilty of is not using automated tests. Ash writes that it’s hard, and it is. We don’t have great tools for this — but that’s no excuse. (And enthusiasm for testing should encourage tool-makers to create better tools.)

A lot of things are difficult (though not impossible) to write tests for: asynchronous code; anything that relies on database state on a server; user interface. (Is that animation smooth or jerky? How do you test that?)

Yesterday I fixed a bug in my code where it was doing database access on the main thread. (One of my rules is that database access on the main thread is never allowed.) I could have written a unit test for this — but it’s more likely I would have just tested that it fetched from the database correctly. It would have passed.

Instead, I should have used NSAssert. Something like this: <code>NSAssert(![NSThread isMainThread], @"shouldn't be in main thread");</code>.

Using NSAssert is <em>easy</em>. It also serves as a form of documentation.

While I don’t disagree about unit testing, I suggest that using NSAssert more often would be a great first step. I myself don’t use it often enough.

I’d also add a bunch of other sins. They may not be deadly, but they’re sins:

1. Not turning on <a href="http://boredzo.org/blog/archives/2009-11-07/warnings">Hosey-level warnings</a>.

2. Not treating warnings as errors.

3. Not fixing every single static analyzer issue.

4. Not downloading crash logs from iTunes Connect.

5. Putting things in your .h file that shouldn’t be public, that should be in a class extension in the .m file.

6. Using short variable names like <code>img</code> and <code>btn</code>.

7. Not using <code>#pragma mark</code>.

8. Not understanding the concept of designated initializers.

9. Using tap gesture recognizers when you need a button. (Think of accessibility.)

10. Not de-queuing table cells.

15. Calling viewDidLoad from your own code.

13. Passing model objects to a <code>UITableViewCell</code> subclass.

11. Not using <a href="http://fishbowl.pastiche.org/2002/10/21/http_conditional_get_for_rss_hackers/">conditional GET</a> for web resources that might not change.

12. Not testing with a clean install.

14. Not using curly quotes — “” and ‘’ — in text that users see, including error messages.

16. Breezy and unnecessary comments like <code>//nil it out, kemo sabe</code>.

17. Not using <code>NSLocalizedString</code>.

18. Using <code>false</code> and <code>true</code> instead of <code>YES</code> and <code>NO</code>.

19. Not testing performance with Instruments.

20. Not analyzing memory use and looking for memory leaks with Instruments.
