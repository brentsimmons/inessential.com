@title Mark on Subclassing
@link http://www.markbernstein.org/Mar14/Subclassing.html
@pubDate 2014-03-16 17:46:55 -0700
@modDate 2014-03-16 17:46:55 -0700
<a href="http://www.markbernstein.org/Mar14/Subclassing.html">Mark Bernstein on Subclassing</a>:

>But <em>both</em> kinds of controller have something in common: their views fit into the right panel of the GetInfo popover. So there’s lots of stuff that they share in order to manage the view and in order to talk to the rest of the system. The common stuff – the stuff about being a swappable Get Info pane – belongs to the superclass. The specialized stuff – books, maps, texts, tf-idf similarity measuring – belongs in the individual pane controller.

He’s right. While in general I tend to avoid subclassing my own classes, there are times when it’s the right design.

This is particularly true when you have a design where the parent class doesn’t actually work (or nearly work) on its own, when it’s there to provide some shared code that all the subclasses need. In that case it would be dumb to duplicate that code, and just as dumb to stand on your head to avoid duplication.

It’s just that it’s not the thing we should always turn to *first* when doing design.

And, as Mark points out, subclassing framework classes (except those designed for subclassing) is a terrible idea.
