@title Crash Catcher for NetNewsWire?
@pubDate 2018-11-27 22:17:50 -0800
@modDate 2018-11-27 22:17:50 -0800
An actual conversation:

<em>Brent Simmons [9:40 PM]</em><br />
**Crash catching** What are people doing for this? NetNewsWire needs something, I suppose.

<em>Wise, Super Old Developer [9:42 PM]</em><br />
Just don’t ship crashing bugs.<br />
Duh.

<em>Brent Simmons [9:42 PM]</em><br />
Well, I don’t, but the system will enforce some amount of crashing, and I want to be able to file Radars.

<p style="text-align:center">* * *</p>

Well that’s me being a total jerk. It’s also a measure of my confidence (sure, let’s call it that) in my not shipping crashing bugs.

But it’s worth remembering — here in the real world, outside of a developer’s chatroom — that there are plenty of programmers who *think* they don’t shipping crashing bugs, but do.

And, despite my confidence, the responsible thing is to include some kind of crash catcher.

<p style="text-align:center">* * *</p>

I want something lightweight. Ideally it just opens a new message in Mail with the recipient, subject, and body set. (I could write that UI part myself, if needed.)

It has to be open source, since I’m not going to include any mysterious binaries in an open source app.

What should I do? Is [PLCrashReporter](https://www.plcrashreporter.org/) the best bet? Or…?
