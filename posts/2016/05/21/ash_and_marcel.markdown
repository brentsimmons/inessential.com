@title Ash and Marcel
@pubDate 2016-05-21 10:15:53 -0700
@modDate 2016-05-21 10:15:53 -0700
Ash Furrow, <a href="https://ashfurrow.com/blog/adulterated-objective-c/">Adulterated Objective-C</a>:

>…maybe it’s not important to re-invent Objective-C’s dynamic runtime in Swift. The language is far more static than Objective-C. And besides, a dynamic runtime is only a set of tools used to solve problems. In a different context, like Swift, different tools might be better suited.

Problems currently solved with dynamic programming should have solutions just as good (if not better) in Swift and future Swift-only app frameworks. And “better” can’t mean, “Yes, it’s a big pain now and inelegant, but the compiler’s happy.”

I’m skeptical that there is a solution short of adopting the same kinds of dynamic features Objective-C has, but I’m only skeptical. I don’t say it’s impossible. I want to be surprised and amazed.

<p style="text-align:center">* * *</p>

Marcel Weiher, <a href="http://blog.metaobject.com/2016/05/what-missing-in-discussion-about.html">What's Missing in the Discussion about Dynamic Swift</a>:

>The truly amazing thing about KVC, CoreData, bindings, HOM, NSUndoManager and so on is that none of them were known when Objective-C was designed, and none of them needed specific language/compiler support to implement.

>Instead, the language was and is sufficiently malleable that its users can think up these things and then go to implement them. So instead of being an afterthought, a legacy concern or a feature grudgingly and minimally implemented, the metasystem should be the primary focus of new language development. (And unsurprisingly, that's the case in <a href="http://objective.st/">Objective-Smalltalk</a>).
