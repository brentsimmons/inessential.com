@title Surviving UI Programming
@pubDate 2014-04-23 15:30:06 -0700
@modDate 2014-04-23 15:52:07 -0700
I’ve often wondered why UI programming is less fun than everything else.

My theory is that it’s because so much of it is arbitrary, single-use programming — I’m making a specific screen or view work the way it needs to, and there isn’t much that can be re-used. There are only rarely generic problems to solve. (Those generic problems are mostly solved — that’s what UIKit is for.)

Luckily, UI programming has gotten easier. These days we have view controller containment, custom view controller transitions, auto-layout, and, especially, appearance controls.

One of the nicer additions is editing static table views in storyboards. I’m doing that right now.

To make UI programming as smooth as possible I try to use all the things designed to make it easier. Stick with standard controls as much as possible. Use storyboards.

But it seems inevitable that there will be some point where I get frustrated. Right now it’s this: I have a grouped table view, a static table, and I want to add a *section* footer. (Not a table footer.) There’s nothing built-in to storyboards for this. ([Please correct me if I’m wrong](https://twitter.com/brentsimmons).)

To make matters worse: I don’t know how big the footer will be. It should be a container view that holds a UILabel with text that uses a custom font. The UILabel, and the container view, should be the exact height needed and no taller or shorter.

I *think* that the modern way is to add auto-layout margin constraints to the UILabel and the container view will tell me its proper size. But I worry that I’ll spend half a day on this, not get it to work (even if there *is* a way to get it work), and I’ll end up punting: doing a view that draws text in drawRect, and getting its size by measuring the text. I don’t *want* to do that, but I’ve done it plenty of times before, and I know it works.

So I think my problem is really anxiety. I expect to get frustrated.

And I have reason. Just last night I was attempting to add a button to a navigation bar. I created the button, then made a UIBarButtonItem with the button as the custom view, then added it as leftBarButtonItem.

The button worked — you could tap it and the right thing would happen — but the text of the button was never actually visible. I spent an hour, and I couldn’t explain it. (I finally just gave up.) (I even tried embedding the button in a container view and adding that instead. I gave the container view a background color. So I ended up with a red rectangle in the navbar but still no button text. Yes, the button was a subview of the container view.)

I’m not new to this. I had an app on day one of the App Store. And if you look at Vesper I don’t think you’ll think, “Oh, this app was clearly made by someone who gets anxious when he writes UI code.” There’s a *ton* of custom UI in Vesper, and I’m very proud of it.

But still: here I am, today, looking at something that should be simple — some text as the footer of table section — and wondering how long it’s going to take me, and wondering if I’ll have to give up on the right way and do it the old-fashioned way.

It’s possible that this just means I should spend more time doing UI programming.

<i>Update 3:50 pm</i>: [John Siracusa on Twitter](https://twitter.com/siracusa/status/459101201154723840):

>@brentsimmons The problem with UI prog. is you’re building on top of the deepest, most opaque stack of code you didn’t write and can’t see.

Exactly right. I think the only remedy is experience. But, the thing is, I *have* a bunch of experience.
