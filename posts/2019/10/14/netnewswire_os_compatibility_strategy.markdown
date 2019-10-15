@title NetNewsWire OS Compatibility Strategy
@pubDate 2019-10-14 17:30:04 -0700
@modDate 2019-10-14 17:30:04 -0700
We have two goals with the app: 1) get as many people using RSS as possible, and 2) make the best app we can.

To reach #2 — making the best app we can — we need to do a couple things. One is stay modern: use new APIs and tools that make the app better and easier to maintain. A second is to not spend time on things that don’t make the app better. A third is to attract and retain contributors, who are usually more psyched to work with modern stuff than with old stuff.

You can see how that’s in a little bit of conflict with #1 (getting as many people as possible using RSS readers).

#### Here’s the plan

After a major OS update, we will switch to requiring that update on our next major release — where major is defined as something like 5.0 or 5.1, but not something like 5.0.1. (In other words: the upcoming NetNewsWire 5.0.3 release will run on Mojave, while NetNewsWire 5.1 will require Catalina.)

At the same time, we will make older versions available via the website. For instance, the last version that will run on Mojave will likely be 5.0.4 (which isn’t finished yet) — and we’ll make that version available indefinitely for people who haven’t upgraded to Catalina.

This will mean that people running older OSes will still get a high-quality app — it’s just that it won’t have the latest features.

The key is that this allows us to make NetNewsWire the best app it can be, and making the best app we can is also part of furthering the goal of getting as many people as possible using RSS. (The biggest part, in fact. Bigger than compatibility with older OSes.)

While I know this will disappoint some people, I hope you’ll understand *why* we decided to do it this way. Decisions like this are never easy — there are always conflicting values to weigh, pros and cons and add up — and we don’t make them impulsively. But making NetNewsWire the best app it can be has to be job #1.
