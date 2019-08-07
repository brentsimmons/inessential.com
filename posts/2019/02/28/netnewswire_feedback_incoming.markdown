@title NetNewsWire Feedback Incoming
@pubDate 2019-02-28 13:49:49 -0800
@modDate 2019-02-28 13:51:59 -0800
I’ve been getting more NetNewsWire feedback now that I’ve called it [actually usable now](http://inessential.com/2019/02/25/netnewswire_5_0d16_actually_usable_now).

Feedback is *always* an education. (See the [most recent issues](https://github.com/brentsimmons/NetNewsWire/issues) for some of it.)

There are things I expect to see, and then do see. Things I expect to see, and then don’t see. And things I didn’t expect at all.

It’s a great reminder that everybody’s different, and people want different things. They want to use the app the way they want to use it.

The tricky part is deciding what to do, of course. When I was younger, and selling NetNewsWire, I was reluctant to add features and preferences — but I did it anyway. A lot. I wanted people to buy the app!

But it did mean that NetNewsWire became, in at least one person‘s words, a kind of “Swiss Army knife” of RSS readers. This made it difficult to move forward with new features that I thought would be cool and useful.

Now that I’m older, and I’m not trying to please everybody and make money, I’m even more reluctant. I want to keep the app as simple as possible — because I like simple apps, and because it means I have time to add other features that I’ve never done before, but that I always thought would be cool.

But, at the same time, I really *do* want it to be used by as many people as possible. So there’s a tension there which I find interesting. My position on it is just to go slowly — which I can’t really help anyway — and think hard about each issue.

#### One That I Did Not See Coming

One of the unexpected things is [Add way to see how many total unread items there are within the app](https://github.com/brentsimmons/NetNewsWire/issues/568).

There *is* a way, of course. There are *two* ways, even: the unread count appears in the Dock icon and beside the All Unread smart feed.

You’d think that would be enough — but it’s not. Consider that you might have the Dock hidden, and consider that you might have enough feeds and folders in the sidebar so that you can’t see the All Unread smart feed — it’s scrolled off.

Then what?

It could go in the toolbar — but some people run with the toolbar hidden. And, anyway, I never like status-y stuff in the toolbar. It could be a non-default toolbar thing — people could add it. But I’ve learned that lots of people don’t know you can customize toolbars.

How about a status bar at the bottom of the sidebar that can’t scroll off? Older versions of NetNewsWire had this.

Sure — but the trend these days, which I like very much, is to have a clean bottom edge to the window. No chrome. Look at Mail, Safari, Pages, and Numbers.

Well, okay — do that, but make it a View menu option, off by default, so we keep the clean edge.

Ugh. Now we’re going down the road of endless permutations of little things you can configure. That’s the road I want to avoid as much as possible. Do we really add that just because of the probably rare case where someone hides their Dock *and* the All Unread smart feed is scrolled off?

Another idea: that bottom-of-the-sidebar status view could appear *only* when the All Unread feed is scrolled off. But I really hate non-stable UI with weird little changes like that. It always seems too clever, and it makes me think the designer thinks they can paper over a design flaw by showing off.

Or there could be a non-scrolling indicator at the *top* of the sidebar. That ruins the nice line going along the top, though. But maybe the timeline needs a thing at the top for sorting, so maybe that line will go away anyway? And: wouldn’t this look weirdly redundant when the All Unread feed is *not* scrolled off?

So… what to do? I’m not actually asking for suggestions — though I’ll get some, because people tend to read things like this as problems-to-solve. (And I don’t mind suggestions. Not at all.) But what I actually intend here is just a look behind the development process at the point where people start giving feedback on an app.

Here’s what happens at this point: your design meets conditions you didn’t account for. They’re often rare cases, but they’re legitimate. And all the options seem pretty bad.

What will probably happen, in this case, is that I’ll punt on figuring it out till after 5.0 ships. I have no idea what I’ll end up doing. Which is part of the fun. :)
