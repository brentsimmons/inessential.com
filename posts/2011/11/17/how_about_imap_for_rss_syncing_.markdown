@title How about IMAP for RSS syncing?
@pubDate Thu Nov 17 11:15:43 -0800 2011
@modDate Thu Nov 17 11:15:43 -0800 2011
On Twitter, <a href="https://twitter.com/maizehughes/status/137191326348357632">Maize Hughes asked</a> about using IMAP. Just store the RSS articles as email on an IMAP server.

He <a href="https://twitter.com/maizehughes/status/137191884773793792">elaborated</a>: “Imagine a desktop Thunderbird install as a mailserver I could get to from my iPhone.”

It’s a creative idea — I like the idea of re-using existing technology — but there are some problems with it. The first obvious one is that you won’t be able to get to your desktop from your iPhone when you’re not at home. (This is true for most people. I’m aware of DynDNS, yes.)

So the IMAP server would have to be on a publicly-accessible server somewhere. And then there are additional problems:

- RSS articles can change. Emails don’t change, once sent.

- You get a lot more RSS articles than email. (Obviously not true for everybody, but generally true.)

- How will the IMAP server get the RSS feeds? Will it fetch and parse them on behalf of all its users? If so, that’s very expensive. If, instead, the clients will send the parsed articles to the IMAP server for storage, that means a lot more work on the part of the clients and a lot more bandwidth used.

- An efficient RSS syncing system would take advantage of the fact that you don’t have to store a given article separately for each different user. If 100 or 100,000 users subscribe to Daring Fireball, it should store Daring Fireball just once, not 100 or 100,000 times. I’m not sure IMAP servers are designed that way.

- RSS articles don’t have reliable unique identifiers. Good feeds do. Bad feeds have unreliable identifiers, and some feeds don’t have identifiers at all.

You could, I think, with a bunch of coding and fitting-things-together, cobble up a syncing system that uses IMAP. But it wouldn’t be very efficient, and it’s not something that would work for general use.

In early 2010 I wrote up an idea for a <a href="http://inessential.com/2010/02/08/idea_for_alternative_rss_syncing_system">fairly simple RSS syncing server</a>. I think it’s a solvable problem as long as you recognize the limits. But I don’t have time to work on it (and I no longer write a client app that would use it). Nevertheless, I still think the best bet is an open source system that is simple and easy-to-install.
