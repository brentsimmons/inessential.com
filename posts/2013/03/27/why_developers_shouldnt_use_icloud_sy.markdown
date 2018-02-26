@title Why Developers Shouldn’t Use iCloud Syncing, Even If It Worked
@pubDate Wed Mar 27 12:37:28 -0700 2013
@modDate Wed Mar 27 12:37:28 -0700 2013
Yesterday the Verge posted <a href="http://www.theverge.com/2013/3/26/4148628/why-doesnt-icloud-just-work">Apple’s broken promise: why doesn’t iCloud ‘just work’?</a>

It’s not the first article on the topic — <a href="http://storify.com/Jury/the-trials-of-icloud">bits</a> <a href="http://www.jumsoft.com/2013/01/response-to-sync-issues/">and</a> <a href="http://createlivelove.com/246">pieces</a> of this issue have come up before. But The Verge did an excellent job putting it all together. Good reporting.

Here’s the thing: if you’re a developer, you shouldn’t use iCloud syncing anyway. I’ll explain.

#### Android and the web

You may think you’ll never want an Android or browser-based version of your app. But are you sure? Really, really sure?

You hope your app will be a hit. (If not, then quit writing it and choose something else.) If it’s a hit on iOS, it could be a hit on Android too — and you can bet that customers will ask for a web app version.

You don’t want to limit the success of your app just because you didn’t want to write your own server.

And even if you’re sure that you’ll never want an Android or web version, is it possible you’d want a Mac version that isn’t sold on the App Store? (Only App Store builds are allowed to do iCloud syncing.)

#### Social software

We’ve been living in a social world for years. But iCloud syncing is not social: it’s per-user syncing.

If you write your own server, you can write the social bits, so your users can share recipes, weather forecasts (look, Mom, it’s going to be sunny on Thursday!), favorite articles, or whatever-it-is your app does.

People *expect* social.

#### Additional services

If you’re writing an RSS reader, you can’t ask iCloud to download feeds.

iCloud can’t poll Twitter to see if your follower count has gone up or down. iCloud can’t <a href="http://forecast.io/">generate weather forecasts</a>. iCloud can’t <a href="http://www.sailwx.info/">track ships</a>.

There are all kinds of services that make sense on the server side. You could do some of them on a client, but at the expense of timeliness and battery life. If it’s a good idea, and you don’t do it on a server, your competition just has to write a server that does it, and your app is finished.

#### Learning how people use your app

You shouldn’t look at private data.

With Glassboard we made the decision — there was no debate — to encrypt messages in the database, so that we couldn’t see private data.

But we could still look at aggregate data. It was interesting to know how many boards were created each day, how often people used invitation codes, and so on.

There’s no substitute for learning about how people use your app. You can <em>guess</em> how people use your app. You can — and should — get all the feedback you can via email, Twitter, and App Store reviews.

But seeing actual data makes a real difference, because it helps you figure out where your resources need to go.

#### Costs

It used to be expensive to develop, run, and maintain your own server. You’d buy a machine or a few machines, get them installed in a data center, figure out how Apache works, install MySQL, and write a ton of scripts. Perl or PHP scripts, most likely. (Ugh.)

You’d use Subversion (if you were lucky) or cvs. You’d write your own testing system from scratch. You’d write a bash script that copied the files up to the server.

And you’d spend a bunch of money.

<em>Everything</em> has gotten easier and cheaper. These days you’d run services on <a href="http://aws.amazon.com">Amazon</a>, <a href="http://www.windowsazure.com/en-us/">Azure</a>, <a href="https://www.engineyard.com">Engine Yard</a>, or <a href="http://www.heroku.com">Heroku</a>. Or get a virtual server on <a href="http://www.linode.com">Linode</a>. You’d choose from one of the many excellent systems like <a href="http://rubyonrails.org">Ruby on Rails</a>, <a href="http://www.sinatrarb.com">Sinatra</a>, <a href="http://nodejs.org">Node.js</a>, and <a href="https://www.djangoproject.com">Django</a>. You’d deploy via <a href="http://git-scm.com">git</a> or <a href="http://mercurial.selenic.com">Mercurial</a>.

If you can learn Cocoa, you can learn this stuff. (And so much of it is wonderful — you’ll <em>enjoy</em> learning it.)

#### Control

Tim Wood, CTO of The Omni Group, tweeted the very wise words: <a href="https://twitter.com/tjw/status/289230416064425984">Own the Wheel</a>.

Here’s the thing: half the mobile revolution is about designing and building apps for smartphones and tablets.

The other half is about writing the web services that power those apps.

How comfortable are you with outsourcing half your app to another company? The answer should be: not at all comfortable.

Do it yourself.
