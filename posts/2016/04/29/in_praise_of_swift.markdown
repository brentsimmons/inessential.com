@title In Praise of Swift
@pubDate 2016-04-29 14:05:14 -0700
@modDate 2016-04-29 14:05:14 -0700
In [Performance These Days](http://inessential.com/2016/04/21/performance_these_days) I argued that developer productivity is more important than the speed of a given language.

And while I wish for an Objective-C *without* the C and *with* the cool parts from Swift, I also realize that it’s not going to happen, and I’m fine with that.

<p style="text-align:center">* * *</p>

I’m at the point where I get *bugged* if I have to write Objective-C code.

I don’t think I’m actually more productive in Swift yet, but that’s not the fault of Swift — that’s just how it goes when you switch languages and the previous language was your primary language for more than a decade.

Writing Swift code feels like driving a hot rod. Sometimes it feels like driving a hot rod into a brick wall. But still: <em>it’s a goddamn hot rod</em>.

If I had just two feature requests, they’d be:

1. Allow `Set<SomeProtocol>`. This is a major part of protocol-oriented programming for me. Comes up all the time.

2. Support KVC. (Note that I specify KVC and not KVO, which I don’t care for.) I use KVC only rarely, but <a href="https://gist.github.com/brentsimmons/47fa9c49cf4efb8e024541d651b6ebd2">when I use it</a> it saves a ton of tedious, error-prone code.

Both of these issues keep me tied to some degree to Objective-C — or at least to NSObject and the Objective-C runtime — for now.

<p style="text-align:center">* * *</p>

Okay, I have a third feature request. And it’s a big one. It’s kind-of for the Swift team, but it’s really for everyone who works on developer tools at Apple.

I’d like to see those teams look at a whole bunch of actual Xcode projects and source for shipping apps and do some analysis. Where do developers struggle? What takes too much work?

The goal is to use these projects to keep answering the question: how can writing high-quality apps be made easier?

It’s not enough to look at apps written inside Apple — these apps should come from outside. I’d bet that many developers would be happy to (confidentially, of course) submit their projects for this effort. I certainly would.

And it’s not enough just to hear what developers say. (Though that’s important too.) There’s no replacement for seeing what they actually *do*.

It’s kind of like when you work on performance issues. You may think you know what’s slow, but there’s no replacement for actually running the profiler and *seeing* what’s slow. Same with this: there’s nothing like actually seeing what problems need solutions.

Maybe this is already being done and I just don’t know about it. If so, then cool.

<p style="text-align:center">* * *</p>

Did I mention that Swift is a hot rod? And I need to go work on some Objective-C code, and I’m procrastinating because it’s Objective-C and I want to go drive my fast car instead.

PS Daniel Jalkut <a href="http://indiestack.com/2016/04/test-with-swift/">suggests writing unit tests in Swift</a>. Me, I’m writing all new code in Swift. But if you haven’t started writing with Swift yet, then you should listen to Daniel.
