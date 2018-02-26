@title App Idea: Mentions
@pubDate 2018-01-09 13:33:23 -0800
@modDate 2018-01-09 13:33:23 -0800
“Hold on — I need to check my Mentions.”

Ten years ago or more we had several blog-specific search engines and services: Technorati, BlogBridge, and others.

One of the great things about these services was not just being able to search for something but being able to set up *persistent* searches: that is, you’d get a search as an RSS feed, and in your feed reader you’d get results from all over the place on the thing you’re searching for.

In the obvious and common cases, you’d set up searches for people linking to your blog, writing about the apps you work on, mentioning the place where you work, and mentioning *you*.

I’d like to see something like this for today, but where the scope is just the Apple/Mac/iOS community. It would crawl the obvious sites (such as Daring Fireball and Loop Insight) and it would crawl the many blogs and microblogs that make up the community.

I *think* this is best as a web service, though it could have Mac and/or iOS client apps. It needs to provide feeds for people using feed readers.

<p style="text-align:center">* * *</p>

With that reduced scope, and with the better tools and cheaper cloud computing these days, I don’t think it would be terribly expensive. Not like it was 15 years ago.

You might want to make money with this, though, and there are a few ways to do it: charge extra for things like notifications and email alerts. Charge money for client apps. Make the first three search feeds free, and charge money for a ten-pack of searches. Etc.

<p style="text-align:center">* * *</p>

An alternate version of this idea isn’t a web service — it’s a Mac and/or iOS app that does the crawling. A kind of specialized Mac/iOS feed reader.

The list of feeds-to-crawl would probably just be an [OPML](http://dev.opml.org) file on the web, and the app would periodically grab that list.

(If you did this, you could use <a href="https://github.com/brentsimmons/RSParser">RSParser</a> as starter code, since it parses OPML, RSS, Atom, JSON Feed, and RSS-in-JSON.)

This would make a great open source project, but it could just as well be free or for-pay.

<p style="text-align:center">* * *</p>

One challenge is handling spam and abusive or hateful content. You’d most likely want to have a suggest-a-site form, so you don’t have to go out and find every single site there is.

But you have to be able to say no, and you have to be able to update the list of sites-to-crawl quickly if a site turns bad or inappropriate somehow.

You’d also need a way for users to report an issue.

(Again, the reduced scope — Apple-related blogs — makes this somewhat easier than if you tried to do the entire blogosphere.)

<p style="text-align:center">* * *</p>

I want this! I’d use it every day. I know other people who would too.

But I’ve got enough on my plate that there’s no way I can do it myself — though I’d be happy to answer questions and provide feedback to anyone who does want to do it.
