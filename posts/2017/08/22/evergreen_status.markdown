@title Evergreen Status
@pubDate 2017-08-22 13:22:06 -0700
@modDate 2017-08-22 13:23:12 -0700
The current goal is a Spring 2018 release of <a href="http://ranchero.com/evergreen/">Evergreen</a> 1.0. Which is rather ambitious, I know, and I wouldn’t be shocked if it was Spring 2019. But that’s the goal.

<a href="https://github.com/brentsimmons/Evergreen">The build is currently broken</a>, has been broken for months, and will continue as broken for at least another few weeks.

Here’s the scoop: I decided to do syncing in 1.0. It will probably be just one system at first (most likely <a href="https://feedbin.com/">FeedBin</a>, since that’s what I use) — but this meant looking at the data and database level and figuring out what’s needed to make it usable when syncing. I’m in the middle of making the needed changes.

(Originally each syncing system was going to have its own database code, but I realized that that would be foolish.)

And, because I’m such a weird database-code-loving freak, I’m not using Core Data. (Total dummy, me. Don’t tell me.) An example is <a href="https://github.com/brentsimmons/Evergreen/blob/master/Frameworks/RSDatabase/RSDatabase/DatabaseLookupTable.swift">DatabaseLookupTable.swift</a>, which manages relationships.

<p style="text-align:center">* * *</p>

Progress is slow, since I don’t get to work on it every day, and even when I do it’s often just for half an hour. There are occasional days where I get a few hours. But, except when I’m on vacation, progress is steady — and that’s how you get things done. (It helps to be obsessed.)

(<a href="https://github.com/brentsimmons/Frontier">Frontier</a>, meanwhile, is on the back burner — I picked Evergreen to ship first just because it was further along. I’ll get back to it.)
