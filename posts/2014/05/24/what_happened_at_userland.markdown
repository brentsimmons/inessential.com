@title What Happened at UserLand
@pubDate 2014-05-24 16:21:48 -0700
@modDate 2014-05-24 16:28:54 -0700
I worked at UserLand from 1996 to early 2002. This article is going to make it sound great — for the simple reason that it *was* great.

(Obviously this is all from my memory and my perspective.)

#### 1996

I was a fledgling indie. I wrote a few little things that worked with WebSTAR, the Mac http server. One of those was a website searching system called Spotlight, which used UserLand Frontier and Filemaker Pro.

I was becoming active in the Frontier community, which was mainly a discussion mailing list. Frontier, previously an app that cost hundreds of dollars, had become free in 1995.

I worked with Dave Winer, UserLand CEO, on the 24 Hours of Democracy project. My part was an app that took submitted text and created a web page. People told their stories about what democracy meant to them. All the pages were linked together so you could step through them.

Dave and I worked well together and the project was a ton of fun. Not long after that I started working as a contractor. Later — I forget when, precisely (1997?) — I became an employee.

I had no formal training in computer science. I just had what my parents had taught me. I don’t think anybody else in the world would have given me a shot. But Dave did.

#### Background on the Tech

Kids these days don’t know what Frontier was. To describe it briefly is to gloss over what was delightful about it, but I’ll do it anyway.

It was a developer tool — a Mac app — that included an integrated environment. It was all one piece. It was started in 1989 (I think) — before AppleScript, long before Macs became Unix systems.

It was early NoSQL. It was a schema-less database built on tables. Tables could contain other tables — and scalars, scripts, outlines, text-editing windows, and so on. It was all exposed in the user interface: you could browse the database, open tables in separate windows, open scripts, etc.

Scripts were written in an outliner — which sounds weird until you try it. It was very cool.

The scripting language, UserTalk, was in some ways like a simplified C. Easy to pick up.

Database access was simple — it used dot notation. If an object named “baz” was in the “bar” table which was in the “foo” table, you’d access it as foo.bar.baz.

There were plenty of built-in verbs and suites of scripts. It did IAC — which meant you could script your apps as easily (more easily, I’d argue) as you could with AppleScript. (Frontier was, in a way, the long-promised “programmer’s dialect” of AppleScript.)

It was a remarkable app. You could build really cool things very quickly. I loved it. (Still do.)

#### Beleaguered Apple

It was 1997, I think, when we had a team: me and Dave, Doug Baron (who’d worked at UserLand in early days), and Bob Bierman. We were working on Frontier 5 — which would also ship on Windows.

Frontier had been a Mac-only app for its entire career. But it was clear that, for the product to survive, it needed a Windows version, since the Mac market share was clearly dwindling.

As a Mac guy this pained me. Those were dark days for the platform.

Doug and Bob did the Windows programming. (Later on we added more people to the team: André Radke, [Jake Savin](https://twitter.com/jsavin), Robert Scoble, and John Robb.)

I don’t recall when it shipped. Maybe 1998. 1999? It shipped on both Windows and Mac. At that point Frontier became a for-pay app again. And it looked like a healthy product with a future.

#### I claim credit for nothing

But while that was happening, and as we shipped follow-ups, Dave was on a brilliant streak. It remains my pleasure to have been there for it.

None of it was mine — but I was privileged to often be the first to hear about something, to sometimes talk things over before the world knew about them.

The way invention works in computer science (as in many disciplines), you can’t necessarily always say who invented what. (Sometimes you can.) But there’s no question that Dave invented some things and popularized and fleshed-out other things.

Here’s the sequence, as I recall it:

• Templated websites. AutoWeb, a set of Frontier scripts, was the first example I know of for building static sites with templates and scripts. This was followed by Frontier’s website framework. In the mid-’90s people thought websites had to be hand-crafted. It may seem incredible now, but lots of people — some of them influential and very intelligent — were deeply skeptical about this idea.

• Weblogs. [Scripting News](http://scripting.com/) existed before the term “weblog” was coined. (Coined by [Jorn Barger](http://en.wikipedia.org/wiki/Jorn_Barger).) It wasn’t the only such weblog — but it helped popularize the form, and UserLand published scripts that made it easy to use Frontier as a weblog authoring and publishing tool.

• RSS. The original format was a pretty simple array of links formatted in XML. Invented at Netscape for their portal. Dave saw the potential in it — and moved the format forward. He wrote some of the first RSS readers, and RSS output was added to our blogging engines.

• Podcasting. Adam Curry wondered about the “last mile” problem — how do we get rich content to people at home on slow connections? (Recall that broadband was much less prevalent in the ’90s.) Dave’s answer: an enclosure element in RSS. The RSS reader running on your local machine would download those enclosures at night, while you slept. I think it was Adam who came up with the name “podcasting.”

• OPML. Frontier was built in many ways around the concept of outlining, and OPML is a document format for outlines. It happens also to be useful as a way of specifying an RSS subscription list, but that wasn’t its original point.

• Hosted blogging for everybody. I was in charge of shipping Manila, which was an online, dynamic website with blogging and CMS features. It shipped shortly after Blogger. (I don’t think Blogger had hosted blogs at first — it worked by FTPing to your own site.) EditThisPage.com let you set up your own blog. There were “Edit This Page” buttons everywhere — the idea being to make blogs and websites simple enough for everybody to write and publish. To sign up — which was free — you created an account and chose the “foo” part of foo.editthispage.com. (Some people and sites you’ve heard of got their start there: Daily Kos, Joel Spolsky, Robert Scoble, Doc Searls, and so on. This site was originally a Manila site: it was created fairly early during Manila development.) This was long before Tumblr and Wordpress — even before Movable Type.

• XML-RPC. It was like JSON before JSON. The idea was that you could serialize just about anything using XML. It had a date type, which I still wish JSON had. Alas. (Says a guy who’s been dealing with a lot of JSON and dates lately.)

• External website editing APIs. Blogger had a simple XML-RPC-based editing API. We extended it, and then wrote a huge API for Manila, and an external client (written in Frontier) so you could edit just about everything. Not just blog posts but pages and templates too. This is an area where the world is still catching up. (MarsEdit still uses the original extended MetaWeblog API.)

• Desktop RSS readers. The first one that I know was Radio UserLand, which was a blogging system that output a static site and that also included an RSS reader. (On the grounds that bloggers also read blogs, and often want to blog about the things they read. It was because of this that NetNewsWire 1.0 also included the blog editor that later became [MarsEdit](http://www.red-sweater.com/marsedit/).) Radio UserLand ran as an app on your desktop but had a browser-based interface. I didn’t work on Radio UserLand that much — that was Dave and Jake Savin more than me. But it was Radio UserLand that got me hooked on RSS.

I’m skipping some things (like distributed database updates via XML-RPC). I’m barely going into detail. An excellent book could be written about this period, about how Dave changed the internet.

#### 2002

By early 2002 I was burned out and in bad shape. I felt like I’d been sprinting for years, and the years of adrenaline had taken their toll.

I was 33 years old by then, and I had learned a ton from Dave and my experience at UserLand. I was ready to go indie again.

First thing I did? Write an RSS reader and a blog editor. But this time in Cocoa. I shipped it in early 2003, and it was a smash hit, and I felt great.

But have I done even 5% of what Dave did to change the internet? Nope. It’s only in retrospect that I realize what an amazing streak he was on. The older I get the more I appreciate it.

#### Question I still have

How much of this creative period was due to Frontier itself and how much to Dave?

I think it works like this: Dave was creative and productive, and he had built for himself an environment where he could move very quickly and try lots of things. Each layer built on top of other layers, and he was able to work at a very high level.

The tech was his invention too: he built the thing he needed to be able to build other things.

#### Skepticism

When I was at UserLand I was frequently skeptical of what Dave was working on. But I knew I was young and had little experience, and I was smart enough not to let my skepticism get in the way.

And then Dave was proved right, time after time. (You have no idea how much I disliked RSS for a couple years. I thought it was Dave’s pet distraction, and it bugged me that he wasn’t spending more time helping me ship our other software. I hope I didn’t actually say that to him at the time, but I might have.)

And so I look at what Dave’s working on now — [Fargo](http://fargo.io/docs/whatIsFargo.html) — and I pay attention, because I know his track record.

#### UserLand After Me

Jake continued to work there. Robert Scoble, Doug Baron, John Robb, and Bob Bierman left. (Whether anyone was laid-off of or whatever I don’t know.) UserLand was sold — I think? — or somehow Dave left and it was passed to other hands, where it didn’t thrive. (I didn’t pay attention.)

Dave made Frontier available via the GPL license. The [kernel](http://frontierkernel.org/) is a fascinating historical document. Here’s how we used to write Mac apps. It was minimally Carbon-ized (by Timothy Paustian and a little by me, as the last thing I did at UserLand). But it’s still a WaitNextEvent app. Doesn’t even use modern Carbon timers or HIViews. To reboot it requires rebuilding from the ground up, at this point.

I still keep thinking that we lost something when we lost Frontier as a modern, updated app. It was a remarkable playground, in the best sense, and I’d still love to be able to reboot it as a modern Cocoa app (forget Windows) — because I think the internet would benefit by what people who use it come up with.

It’s inherently geeky, since it’s a developer tool. But at the same time it’s more accessible than text editor + command line + Ruby/Python/whatever. It can give more people a taste of what power on the internet is like — the power to create your own things, to re-de-centralize, to not rely on Twitter and Facebook and Apple and Microsoft and Google for everything.

I have a plan, but it’s long and slow-going. I can’t promise anything.

And maybe that’s just me thinking I can bring about a silver age by using the only skill at my disposal: writing code. But maybe that wouldn’t be wrong, either. Most likely it’s not something I’ll ever complete, which I’ll regret.

#### P.S.

My co-worker at UserLand and friend Jake Savin moved into my neighborhood a few months ago. I see him twice a month at [Xcoders](http://seattlexcoders.org/) meetings. He works at [Black Pixel](http://blackpixel.com/), which now owns [NetNewsWire](http://netnewswireapp.com/), the RSS reader I wrote just after leaving UserLand.

#### P.P.S.

My burn-out at UserLand was in part due to running servers. They were actual machines. We didn’t use a data center — instead, Dave and I each had a T1 to our respective homes. So I had almost a dozen machines running, loudly, in my office. And they required constant care and monitoring.

When I left, I vowed never to be responsible for servers every again.

That vow lasted until [just recently](http://inessential.com/vespersyncdiary).

(Of course, it’s not really the same. I have a couple hosted Node.js sites. No noisy old machines in my office. Giant difference.)

#### P.P.P.S.

The first time I visited Dave’s office I noted his Eddy award statue for Frontier. I remember thinking: “Wow. I’d dearly love to win one of those myself some day. I think I’d just retire happy at that moment.”

Now I’ve got two. And I didn’t retire. :)
