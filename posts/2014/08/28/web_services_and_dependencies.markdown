@title Web Services and Dependencies
@pubDate 2014-08-28 13:11:49 -0700
@modDate 2014-08-28 13:13:10 -0700
Tim Schmitz <a href="https://twitter.com/TimSchmitz/status/504790636974080000">asked me on Twitter</a>:

>Curious on your take on dev services re: social network post. Should devs avoid svcs like Azure because an app may outlast it?

(He’s referring to <a href="http://inessential.com/2014/08/27/waffle_on_social_media">my post from yesterday</a>.)

You can’t escape dependencies — even if you’re running Linux, Apache, MySQL, and PHP on a virtual machine — and so you need to evaluate everything.

Some questions to ask:

How long will this service be around? How difficult would it be to move? How much of this service’s unique features do I use? How much benefit do I get from those?

This extends to software, too. What is a given package’s reputation for security? Is it likely to be maintained in the future? Will upgrading to get a security fix also mean revising some of my code?

You have to plan for scale. Will this service and and those software packages allow room for growth? (Sharding, running multiple instances, etc.)

And you have to balance developer time. The point is to do less housekeeping and more bug fixes and features.

With Vesper we chose <a href="http://azure.microsoft.com/en-us/services/mobile-services/">Azure Mobile Services</a> on the grounds that it’s likely to be around a very long time and it’s based on Node (which is well-supported and runs in many places). The folks there were extremely helpful as we were making our decision, and that helped us decide. (You want to go where you’re wanted, for one thing.)

That said, we still have contingency plans, because anything could happen. There are *no* cases where you wouldn’t want to plan to be able to move. (In fact, we have two: one for moving from Mobile Services to another Node provider and one for moving to another service running Sinatra, in case we have reason to get off Node.)

Our contingency plans aren’t specified to the smallest detail, but that wouldn’t be more than a day of work, which is acceptable. (One reason not to get too detailed: the options will look different in six months, one year, three years, etc.)

I have no expectation that we’ll ever need to move. Azure is a big bet for Microsoft (the new CEO comes from the Azure group). We’ve found that the system performs wonderfully (we get praise for efficient syncing) and there’s a ton of room for growth — we’ve barely scratched the surface so far. (We run with just one instance, and that’s well more than enough.) We’re entirely happy with our choice.

That’s what works for us. But every app and every developer is unique, and there’s no way out of evaluating all the dependencies and making the best decision. I don’t think there are easy answers — it takes diligent research and thinking.
