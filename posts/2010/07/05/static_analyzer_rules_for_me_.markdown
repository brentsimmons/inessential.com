@title Static analyzer rules (for me)
@categoryArray Cocoa-Development
@pubDate Mon Jul 05 15:15:18 -0700 2010
@modDate Mon Jul 05 15:15:18 -0700 2010
I so adore Build and Analyze.

I’ve developed a small set of rules I follow:

1. *Always* run static analysis. There’s a project setting called Run Static Analyzer — if you set it to true, it will always run the analyzer when you build the project. So I set it to true.

2. If the static analyzer finds a problem, I immediately add a <code>TODO</code> comment with a quick note about what needs to be done. Even if I think I’m going to fix it right away. (Because the phone might ring, cat might need dinner, and I’ll forget.)

3. If the static analyzer finds a false positive, I immediately add a comment along the lines of <code>//Static analyzer false positive</code>. This way I don’t waste time on it later, and nobody else does, either. (Ideally there’s an explanation, too, if it’s not self-evident.)

4. But I still consider a false positive a kind of warning. It’s a good sign that something too clever (in a bad way) is going on. So, if I think I should — and I usually should — I also add a <code>TODO</code> comment about revising whatever it was that triggered the false positive.

The goal is, as with errors and warnings, a completely clean bill of health.
