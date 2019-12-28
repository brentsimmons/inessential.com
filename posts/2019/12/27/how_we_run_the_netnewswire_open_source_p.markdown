@title How We Run the NetNewsWire Open Source Project
@pubDate 2019-12-27 16:40:52 -0800
@modDate 2019-12-27 22:03:33 -0800
People ask me, “So — I can just show up, see something I feel like doing, do it, and then it will just show in the app?”

The answer, perhaps surprisingly, is no. Or, mostly no.

Well, kind of yes. It’s complicated. I’ll explain.

### We run the project as if it were a commercial app

There’s a misconception about open source apps: people often think they’re not really intentionally *run* — they just kind of accrete whatever features and fixes that people who show up feel like doing.

NetNewsWire is not willy-nilly like that. We plan features and fixes the same way we would if the app cost money. We have a help book, a website, a blog, a Twitter account. We work especially hard on design. In most respects it’s indistinguishable from a commercial app.

We even set dates internally — and then blow right through them. :)

I’ve become fond of saying that NetNewsWire is a team. It is! But it’s also true that the app has my name on it.

My leadership style is to ask questions, talk things over, look for consensus, and trust people — but the last call is mine. It’s not a democracy, and it’s certainly not a thing where people just show up and ship whatever they feel like.

### We definitely do *not* run the project as if it were a commercial app

But remember that NetNewsWire is free, has no budget (not one cent), and everyone who works on it is volunteering their time.

So there are some things we do differently from a commercial app.

#### Quality

A big one is app quality: we have to do way better than commercial apps.

This may seem surprising, but consider: we don’t have a support team. We help people when they have questions, but it’s vitally important that we ship the highest quality app possible so that we don’t get bogged down doing support. (The Help book is a big part of that too! But we’d do the Help book regardless, because it’s a matter of respect for people who use the app.)

You may remember older versions of NetNewsWire with fondness, and you may be missing some features the older versions had — but make no mistake: NetNewsWire 5 is a *much* higher-quality app than any older NetNewsWires.

And — this is smaller, but real — we publish the source code. Anyone can read it, and we don’t want to be embarrassed by it. Even better: we hope that people can learn from it! I’d bet that the majority of for-pay Mac and iOS apps couldn’t survive this kind of scrutiny. (I don’t say that to be mean. They don’t have to, so they don’t.)

This may sound paradoxical, but it’s true: *because* NetNewsWire is free and open source, we have to have a higher bar of quality than commercial apps have.

#### People show up

I said at the top that people can’t just show up and work on whatever and then we ship it.

Except, well — sometimes people actually *do* show up and work on what they want to work on, and then we ship it.

The difference is planning and design. We talk things over on our Slack group, in the #work channel: is that feature right for the app? Will it perform well enough? Does it depend on something else being done first? What’s the design for the feature? Does it need to go into 5.1, or 6.0, or…? Is it a Mac-only thing, or iOS-only, or is it for both? Etc.

(We also use the GitHub bug tracker and create milestones for different releases.)

Consider the situation with syncing systems. I knew we wanted to ship NetNewsWire 5.0 for Mac with Feedbin syncing. We couldn’t ship with nothing — and Ben Ubois at Feedbin has been super-helpful, and Feedbin is awesome, and so it was a no-brainer.

And then consider that, after that, Feedly syncing was by far the most common request, so it was obvious to prioritize that one next. (The iOS TestFlight build includes Feedly syncing, and the Mac app will follow suit.)

And then consider that our goal is to support all the various systems. Which one will come next, after Feedly? How do we choose? This decision is based in part on people who show up: what systems do they want to work on?

This is not how you’d do things with a commercial app, but in this context it works fine.

By which I mean there absolutely *is* an element of going with the flow of who shows up and what they want to do. That’s actually part of the fun.

#### No Revenue

People have offered money — just in general or for a specific feature. But we won’t take any money at all. Money would ruin it.

When money’s involved, it becomes an *issue*, and in this world it’s *the* issue. We have our own little utopia where we can pretend like it doesn’t exist. (“How fortunate!” you say. Yes, indeed, and we don’t forget that fact for a second.)

This means, though, that our decisions can be entirely about what’s best for the app and the people who use it — we never, ever have to think about what’s best for revenue.

This is so nice!

#### Transparency all the way down

No part of NetNewsWire is behind closed doors. The code is available, the bug tracker is open, and anyone can join the Slack group. You can watch us — and help us! — make decisions.

Because of this, I can’t do that thing commercial apps do where they keep quiet about stuff and then do a big surprise release with a bunch of new features. Luckily, I’ve done that enough in life — I have no interest in doing that over and over.

Instead, we’re honest and open about our goals and what we’re doing and when we’re doing it. Nothing’s hidden.

Which makes me feel sometimes like I’m doing a high-wire act and everybody’s watching. The level of difficulty is certainly higher than with the average commercial app, since we can’t hide our code or our thinking, since everyone is a volunteer, since we have to do *better* than for-pay apps.

But I wouldn’t have it any other way. I have always loved making apps, but making *this* app with *this* team is the most fun I’ve ever had. By far. (And I’ve worked on some pretty great teams.)

And you can [join us](https://github.com/brentsimmons/NetNewsWire/blob/master/CONTRIBUTING.md) if you like! Everyone’s nice. 👍

PS My favorite part of the [page where I announced the TestFlight beta](https://ranchero.com/netnewswire/test-ios) is the Credits, near the bottom. You could be in there next time.
