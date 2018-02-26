@title Subclassing Follow-up: the Solution
@pubDate 2014-03-15 16:11:49 -0700
@modDate 2014-03-15 16:22:47 -0700
In [a previous post](http://inessential.com/2014/03/14/a_case_for_subclassing_) I outlined some options I had for a timeline view controller that has three different configurations.

In the end I settled not on subclassing but on using a delegate. It still felt <em>weird</em>, though, as if this couldn’t possibly be the best solution.

That weird feeling was the right feeling.

#### Qnoid

[Markos Charatzas](https://twitter.com/qnoid/status/444747058214604800), with the delightfully odd @qnoid handle on Twitter (which makes me think of pizza), diagnosed the problem correctly:

>the problem is a creational one i.e. [https://gist.github.com/&#8203;qnoid/&#8203;57c50a629a984209c6b5](https://gist.github.com/qnoid/57c50a629a984209c6b5) … if you are comfortable with Java, related: [http://qnoid.com/&#8203;2010/10/11/Don%27t&#8203;-underestimate-the-factories&#8203;---Don…](http://qnoid.com/2010/10/11/Don%27t-underestimate-the-factories---Don%27t-lose-your-train-of-thoughts.html)

He’s right — the problem is a creational one.

But *factories*?

We Cocoa developers are a pastoral lot — Shire-dwellers — and factories are part of the hellscape of modern industrial languages. Not Cocoa, not Objective-C.

Except that that’s not entirely true. See the docs on [Class Factory Methods](https://developer.apple.com/library/ios/documentation/general/conceptual/CocoaEncyclopedia/ClassFactoryMethods/ClassFactoryMethods.html).

While we’d never create a factory object, we’d add factory methods to a class. Do it all the time.

Here’s what I’d forgotten: class factory methods can be more than a single convenience wrapper for init. Which means I can do this:

<code>+ (VSListViewController \*)listViewController&#8203;ForAllNotes;</code><br />
<code>+ (VSListViewController \*)listViewController&#8203;ForTag:(VSTag \*)tag;</code><br />
<code>+ (VSListViewController \*)listViewController&#8203;ForArchivedNotes;</code>

This has nice advantages:

* Simple API.
* No need to create another object as delegate or configuration object.
* Self-contained — I need only look in VSListViewController.m to find relevant code.

So that’s what I’m going to do.

Now I just wish I knew why I didn’t think of this right at first. Well, next time I’ll remember it.
