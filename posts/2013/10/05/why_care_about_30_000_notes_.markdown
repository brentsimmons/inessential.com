@title Why Care About 30,000 Notes?
@pubDate Sat Oct 05 20:54:53 -0700 2013
@modDate Sat Oct 05 21:13:51 -0700 2013
On Twitter, <a href="https://twitter.com/zvisus/status/386647656040108032">Zvi Zemel asks</a>, regarding my <a href="http://inessential.com/2013/10/05/vesper_sync_diary_2_core_data">previous post</a>:

>@brentsimmons honest question: why are you worrying about performance with 30,000 notes in Vesper? Will anyone encounter that scenario?

When I was a kid back in the ’70s and ’80s I was really into hi-fi systems. I couldn’t afford much gear, but I could borrow copies of The Absolute Sound and read them cover-to-cover. In those days the general wisdom was to buy an amplifier with way more power than you could possibly ever use, because it would sound great at low and normal volumes.

That wisdom stuck in my head, and I think it applies to software.

#### My guess is always wrong

I’ve learned that I’m unlikely to over-estimate the amount of data people like to keep.

Years ago (2005) I added a tabbed browser to NetNewsWire for Macintosh. I guessed that my most extreme user might have as many as 100 tabs, and I needed to make sure it scaled to that.

I released the feature and people liked it. After a while I started getting complaints about performance from people who had thousands of tabs. Some users had tens of thousands of tabs. I was *way off* in my estimate of what the most extreme user might do — and I’ve remembered that ever since. (The app remembered your tabs between runs, which was a fairly rare thing in 2005.)

So now I don’t try to guess what a reasonable extreme might be — I guess what an *extreme* extreme might be, knowing that there’s a good chance I’m still under-estimating.

#### But really — 30,000 notes?

I don’t know who would type in 30,000 notes. That’s a lot of typing.

Since a note can be a photo with no text, there could be someone who makes thousands of notes-that-are-photos.

But still, 30,000 notes is a highly unlikely scenario for an iPhone app.

However — what if the popular Twitter apps had a send-to-Vesper feature? Or if we added a bookmarklet to Safari for iPhone that let you add a page as a note?

Or, going even further: what if we had a public web services API? What if we had a scriptable Mac app? What if some form of scriptability was added to iOS?

Add in automation, and suddenly 30,000 notes doesn’t sound crazy.

I’m not promising or even hinting at anything. I’m just explaining what I think about when I’m making decisions regarding performance and scalability. If I assumed that there would never be a way to automate adding notes, I might be correct — but I’d be guilty of malpractice. The engineering department doesn’t have the luxury of making that assumption.

#### Performance Is Important

I think performance is under-rated by many developers. There are apps that I use and love that block the main thread too often, apps that are otherwise wonderful. I’m disappointed every time I notice. I sigh at the app.

I’m a developer, so I know what’s going on, and I know that it doesn’t have to be that way.

But I also think that non-developers notice these things. They don’t notice an app that performs well — it just works — but they notice an app that doesn’t. And I’m unwilling to let my app be one of those. If one person ever sighs at my app — for being unresponsive to touches, for dropping frames in animations, whatever — then I haven’t done my job.

What makes an app successful? What makes an app do well enough in the App Store so that you make enough money to be able to keep doing what you love?

I don’t know. But I think that frustrating users with non-responsiveness (and, worse, crashes) is a pretty sure way to make an app *not* successful.
