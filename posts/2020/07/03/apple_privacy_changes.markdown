@title Apple Privacy Changes
@pubDate 2020-07-03 17:24:48 -0700
@modDate 2020-07-03 17:24:48 -0700
I was actually surprised at the changes Apple is making to stop tracking. It’s not enough to stop tracking on the web, and it’s not enough to stop tracking in iOS apps — which is happening probably way more than you think it is — so Apple did <em>both</em>.

While I know that Apple takes privacy seriously in a way other large tech companies don’t, I still didn’t expect them to go this far. I’m glad they did.

My pet theory is that this set of changes is the most important thing to come from WWDC this year. These privacy changes will, I think, have far more impact on the tech industry, on society, and on our lives, than SwiftUI or a new processor for Macs or anything like that. (As fun as those things are.)

It’s always going to be an arms race, I suppose — see this [press release from Kochava](https://www.kochava.com/apple-announcements-at-wwdc-2020-challenge-marketers-to-tap-alternative-marketing-solutions/):

> Options exist to perform identity resolution using hashed-email-to-device linkages, device connections by household, and other first-party identifiers key in solving for identity resolution and attribution.
>
> […]
>
> Further scarcity of the IDFA forces greater reliance on attribution by fingerprinting. Fingerprinting is a probabilistic method of attribution based on device IP & user agent that’s less precise than deterministic attribution based on the globally unique IDFA. Nonetheless, a high degree of accuracy is still maintainable with fingerprinting…

IDFA stands for “identifier for advertisers.” One of the changes Apple is making is that when an iOS app asks for the IDFA, the system will ask the user to consent to being tracked. When consent is not given, the IDFA will just be a string of zeros.

It’s self-evident that pretty much everyone will say no, which makes the IDFA useless. App makers will want to avoid even the shame of asking for consent.

Kochava is saying — and I’m betting they’re not the only company saying this — that they’ll find a way around the IDFApocalypse to identify users. They will probably succeed, too, at least to a certain degree.

However, Apple has shown that it has a mandate to fight, and the will, and it doesn’t mind dropping down some very large technical hammers to protect our privacy.

<p style="text-align:center">* * *</p>

It’s important to note — before people get stigmatized unfairly — that most of the tracking and metrics collected by various websites and apps is done so with innocent motives. Marketers want to know which campaigns are more effective; they want to get the most bang for their buck. Product designers want to know which features are more popular; they want to know what’s working for people and what isn’t. Publishers want to know which pages people visit and how they got there. Engineers — like me — want to be warned of potential problems.

There’s nothing wrong with wanting those things! The people who want those things aren’t trying to snoop on people or anything — they’re using data to do their jobs better.

The problem is that the tech industry, in order to serve these needs, did what it always does: code up the thing, take the biggest bite it can, and hope to make enough money, and amass enough power, to be able to repel any future ethical distractions. So now we have mass surveillance.

But Apple recognizes that there’s still a need to know, for instance, which of your ad campaigns is doing best — and so there’s [SKAdNetwork](https://developer.apple.com/documentation/storekit/skadnetwork), which is a thing I don’t totally understand yet, but I get that it answers marketing questions in the aggregate (which is all marketers should want) and doesn’t violate privacy.

I like that Apple knows that it’s not enough to just shut down the bad actors — people who have questions to answer, but who have no interest in violating privacy, need solutions.

PS See the WWDC 2020 video [Build trust through better privacy](https://developer.apple.com/videos/play/wwdc2020/10676/) for way more about all this.
