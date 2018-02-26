@title SCM Search
@pubDate 2015-01-30 10:24:25 -0800
@modDate 2015-01-30 10:24:25 -0800
My co-worker and local hero Curt Clifton <a href="https://twitter.com/curtclifton/status/561041191085412353">writes on Twitter</a>:

>Archiving 24,724 commit message emails to EagleFiler. Maybe Mail.app will actually perform reasonably after this. Fingers crossed.

Here’s the thing: this sucks.

At Omni, like many places, we get commit messages via email. (I have three filters and folders: one for mine, one for OmniFocus, and one for everything else.) It’s fine — email is a decent notification system.

The problem comes when I want to *find* something in a past commit message. Which happens all the time.

What I’d like is a commit-searching app that’s a desktop app (because I’m not going to remember yet another command line app’s arguments) that supports Subversion (which we use at Omni) and Mercurial and Git (both of which we use at Q Branch).

Were I to write this myself (I’m not going to) I’d probably use SQLite to store the messages and their metadata and <a href="http://nshipster.com/search-kit/">SearchKit</a> to make it searchable.

It’s possible that something like that wouldn’t work for Omni — with our hundreds of thousands of commit messages, a database on a server is probably better — but it would work for smaller teams.

Is this a money-making idea? I don’t know. But as a Mac app it would probably do better than whatever iOS app you were thinking of writing. (You’d get *my* money, at least.)
