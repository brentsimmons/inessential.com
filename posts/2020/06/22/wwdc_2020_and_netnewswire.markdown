@title WWDC 2020 and NetNewsWire
@pubDate 2020-06-22 15:59:50 -0700
@modDate 2020-06-22 16:01:14 -0700
I love seeing so much attention paid to the Mac this year!

I’ve applied for a Developer Transition Kit for NetNewsWire. My thinking: since NetNewsWire is open source, other developers can, and do, look at the code to help them write Mac apps. The sooner we have NetNewsWire updated, the sooner it’s available as an example for other developers.

Other thoughts…

The new Mac operating system, Big Sur, big number 11, Onze-y-baby, has some appearance and behavior changes which of course we’ll adopt. One of NetNewsWire’s values has always been to stick pretty close to Apple’s design for the platform. We do that because, well, we figure users of a given platform actually *like* the platform design, and that’s why they picked it. (It also tends to mean less work, which is a good thing.)

We’ll not be switching to Catalyst. It appears to be much-improved, but standards for a good Mac app are high, and I’m skeptical that Catalyst is all the way there yet.

Instead, our plan is to converge our UI code over time by using SwiftUI. This way we can go view-by-view. (It’s worth noting that we already do share some UI code: the article view is mostly shared, for instance, even without using SwiftUI or Catalyst.)

I’m looking forward to the rest of the week. I especially want to hear more about the new outline view in SwiftUI. 🐣🐥
