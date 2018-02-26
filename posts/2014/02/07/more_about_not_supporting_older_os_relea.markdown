@title More About not Supporting Older OS Releases
@pubDate 2014-02-07 15:31:53 -0800
@modDate 2014-02-07 15:31:53 -0800
I heard from an internet pal who told me they had numbers for their app like this:

5% on 10.6<br />
5% on 10.7<br />
10% on 10.8<br />
80% on 10.9

The question is this: is this an exception? Should they continue to support at least 10.8?

No.

(There may be an exception for niche apps — education and enterprise apps, for instance. My “No” applies to the majority of consumer apps.)

Here’s the thing about those numbers: they’re a snapshot. The percentage of people on older OSes get smaller every day, as people do eventually upgrade their OS or buy a new computer.

In three months there might be just 8% on 10.8 — but you’ve committed to coding and support for that dwindling share.

And the big thing looms: 10.10. It will come out later this year. At that point you’re supporting *three* OS releases, which is unreasonable.

When making decisions like this, I don’t think about what conditions are were I to ship today — I think about what conditions will be like when I actually do ship, and I think about conditions six months out as we do support, testing, and maintenance releases.

Given that, anyone working on a Mac app that they don’t plan to ship until Summer might even consider dropping 10.9 — go straight to 10.10. (I know we don’t know anything about it, but you can still plan for this.)
