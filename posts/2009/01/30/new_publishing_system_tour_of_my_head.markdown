@title New publishing system / tour of my head
@pubDate Fri Jan 30 09:29:34 -0800 2009
@modDate Fri Jan 30 09:29:34 -0800 2009
This website and ranchero.com just got a new publishing system.

(Sorry if you saw replays in your RSS reader. New system meant new guids, which could mean items showing up again.)

I’m not going to release the source or anything like that. But a decent respect for the opinions of mankind compels me to explain how I came to dissolve the bonds tying me to PHP and MySQL.

Which is to say — I’m gonna reminisce. And ramble. And not come to an actual point.

#### About the system

<img src="http://inessential.com/images/wildcat_folder.png" alt="wildcat in Finder screenshot" height="561" width="211" align="right" hspace="5" />

It’s written in Ruby, but doesn’t use Rails. It runs on my desktop. Each post is a separate file, and the publishing system renders static pages, which get pushed to the server via rsync.

It’s more than just a weblog system, though: it’s a small content management system, complete with templates and macros and snippets and all that good stuff. I’ll be able to use it to create the help manual for NetNewsWire and to manage the appcast feeds (both of which I’ve been doing by hand, to my <em>extreme horror</em>).

Some benefits:

- I have the entire site on my hard drive.

- The entire site is in source control (git, actually), and so I can do branches and look back at revisions and so on.

- It’s easy to backup: no databases involved.

- I have a staging server: Apache running on my laptop.

- I still write and edit using MarsEdit — all I had to write was write a few XML-RPC handlers.

- But I can also use any text editor when I want to.

- My sites are searchable locally via Spotlight (and grep and find).

- Since it generates static pages, I can move from one web-host to another very, very easily.

If it sounds like a system a programmer would love — well, yep, you’re right.

#### Aside about UserLand Software

Anyone who’s known me a long time remembers UserLand’s website framework. This is very much like that -- and so the design is <a href="http://scripting.com/">Dave Winer</a>’s, not mine. (It’s probably closest to the <a href="http://frontier.userland.com/bbedit/">BBEdit/Frontier system</a> we’d done, since files are on disk rather than in an object database. But that’s also a lot like Radio UserLand, which came much later.)

In case you <em>haven’t</em> known me a long time: I worked at UserLand in the second half of the ’90s, until early 2002.

In case you don’t know what UserLand was — it was the small-but-smart company where half of everything was invented, or at least co-invented, or sparked, or used first, or fleshed-out, or prototyped, or whatever.

We were doing weblogs using templates and scripting back when everyone thought it was crazy, that the <em>only</em> way to go was hand-created sites. Back before the word “weblog” was invented. We did RSS, XML-RPC, OPML, and weblog editing APIs. <a href="http://bhc3.wordpress.com/2009/01/16/before-there-was-twitter-there-was-dave-winers-instant-outliner/">Instant Outliner</a> was like Twitter for workgroups. We had Edit this Page buttons 10 years ago. Etc.

I can’t and don’t claim personal credit for any of this: Dave was the founder, leader, and brains. I was just lucky enough to be there. But hell — that was some <em>good</em> luck.

There were days when I woke up and wondered how we were going to change the world that day.

In case you’ve never had that feeling, let me recommend it to you. It’s awesome. (To Dave I say: thank you for taking a chance on me. I wouldn’t trade my time at UserLand for anything.)

My entire career since has just been building on the technology UserLand pioneered. <em>Lots of people’s</em> careers and businesses have been building on that same technology.

#### 2002: PHP + MySQL

In 2002 I went indie. (We didn’t call it that then, though. It was still, ugh, “shareware developer,” which was just plain incorrect. An awful term.)

I planned to write weblog and RSS software of some kind, so I knew I’d have to create my own weblog system so people wouldn’t think I was biased toward UserLand’s systems. I had to be independent in order to have credibility as a developer. (I had been at UserLand since 1996, and that’s how people knew me.)

So I wrote a system that used PHP and MySQL. It was pretty fun to learn a new language and all that. But I never loved the system that much: it lacked the elegance and power of the systems I worked on at UserLand. It was a pain to extend.

Seven years later, right around lunch-time, I deleted that code.

Which felt <em>good</em>.

#### Cat names

The old system, that I just deleted, was called Tiger. In my defense, I’ve been using cat names longer than Apple, and I’m not going to stop.

The new system is called <a href="http://www.youtube.com/watch?v=Bj1DZKOeZhI">wildcat</a>. (Link courtesy <a href="http://www.red-sweater.com/blog/">dcj</a>.) So I actually get to type stuff like <code>wildcat -p</code> in Terminal. Fun for <em>me</em>, anyway.

<img src="http://inessential.com/images/wildcat_terminal.png" alt="wildcat in Terminal screenshot" height="31" width="385" />

#### wildcat + <a href="http://www.red-sweater.com/marsedit/">MarsEdit</a>

<img src="http://inessential.com/images/wildcat_marsedit.png" height="319" width="396" alt="wildcat in MarsEdit screenshot" />

#### Developer thought stream

Here’s how I came to write wildcat. Either this is an interesting look into how developers think, or it’s just random bullets from a mis-firing brain.

A few months ago I was thinking about a few things:

- I <em>need</em> to write on my weblogs more often. But I don’t because I hate my publishing system. It’s silly to be put off by that, but it was true anyway.

- I really should check out git for its easier branching and merging. Subversion was such a great step over cvs, but some things are still too much of a pain, and I have a <em>ton</em> more need for branching and merging these days.

- I need to learn Ruby or Python. I have a bunch of development stuff to automate, stuff that I shouldn’t be doing by hand.

- I want to make NetNewsWire more hack-able, maybe by embedding MacRuby or PyObjc. But I should probably actually learn one of those languages.

- I can’t believe I update the appcast feeds by hand.

- I can’t believe I update the NetNewsWire help book by hand.

- Did I mention I hate my publishing system? No good backups, no source control. Bad performance of PHP on a busy server. No staging server. Not easy to extend. Doesn’t use Markdown (and I love Markdown). Etc. Ugh.

- Computers aren’t getting faster: we’re just adding more cores. This site isn’t going to get any faster.

- There’s an economic downturn, which means, even if computers were getting faster, people would be slow to buy them. Resources won’t change — but we still want better performance, we want to do more with what we have: what are some of the ways to do that?

Of course, these weren’t the only thoughts in my head. And they weren’t connected to each other.

For a little while I thought about doing a new publishing system in Ruby on Rails. That would be a chance to learn Ruby, and I could possibly even use my MySQL databases without making any changes.

But for some reason that didn’t really <em>excite</em> me, and I was worried that it would be even slower than my PHP-based system.

I kept thinking about the website framework I helped work on back in the ’90s, back at UserLand. I loved that thing and have missed it for years.

Then one day I realized: since I had turned off comments on this site, it didn’t actually need to be generated on the server. <em>These could all be static pages</em>.

And if I did want to have comments again some day I could use a system like <a href="http://www.intensedebate.com/">Intense Debate</a>. If I want to make the site searchable I could use something like <a href="http://www.lijit.com/">Lijit</a>.

So I was off-and-running — or, rather, it was a background process, some fun code to work on when I had a chance. Months later my 800-ish lines of Ruby are good enough to actually build and publish my sites.

#### Languages

And by the way — I’ve enjoyed learning Ruby. Fun language.

But I find I still feel like learning Python too. I just need a project. Maybe a bug-tracker?
