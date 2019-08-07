@title Why NetNewsWire 5 Doesn’t Support Nested Folders
@pubDate 2018-09-09 17:50:05 -0700
@modDate 2018-09-09 17:54:26 -0700
I was asked on the NetNewsWire Slack group about supporting nested folders — folders inside other folders — and I realized the answer deserves a blog post, because it brings up some larger issues.

But first, some technical stuff.

RSS readers have moved over the years toward tagging as opposed to folders.

A structure where feeds can have multiple tags is the same thing as a structure where you have multiple folders but not nested folders, and a feed can appear in more than one folder.

So that’s what NetNewsWire does, because this looks like a de facto standard to me.

That’s part of the reason, but there’s more…

#### Simplicity

In earlier versions of NetNewsWire there were too many features that added to the <em>fiddliness</em> of the app.

Those features were invitations to the user to comb and revise their system. They could customize colors and fonts, create deep folder structures, archive articles on disk, and so on.

Over the years I’ve learned that these kinds of things often detract from an app. Every decision is a moment of anxiety for the user. The user wonders: is this the right call? Did I consider all the issues? Can I change it later?

And the user may be motivated to come back and re-do those decisions.

I don’t want my software to do that to you.

Furthermore: simplicity is itself appealing. Delight comes in getting the most power from the smallest effort.

Adding features may make the app more appealing to people who want those specific features — but it chips away at simplicity as a feature, and some people will go look for something less complicated.

To be clear, though, this approach isn’t right for every app. It depends on what you want the app to be. I like [Acorn](https://flyingmeat.com/acorn/) for its relative simplicity over Photoshop, for instance — but Photoshop absolutely needs to be what it is for people like [Brad Ellis](https://twitter.com/bradellis) to get their work done.

I have the luxury of not needing to make money from this, and I also have the luxury of knowing there are other really good RSS readers. I’m not required to make this particular app *the* RSS reader for every single person.

#### Bugs

Our industry has not only been poor ethically, it’s also been substandard at just plain old *quality*. Sure, the economics of it are partly to blame. It motivates people to sell out their users and to ship broken software.

“Move fast and break things” is a motto that seems to apply to the industry at large. I think it’s wrong, because there’s a human cost to this.

Again — because I have the luxury, because I don’t have deadlines or commercial concerns — I can do something different: I can ship software with no bugs. Zero.

I’ll be more precise: if a bug is any ticket in the issue tracker, then of course there are always bugs. I’m talking about known, reproducible defects.

My plan is to never release a shipping version that has any such defects. I believe that’s a feature in itself.

But that’s much more easily done with a simpler app. Every added feature adds to the combinatorial complexity of the app, and the app becomes harder to test and harder to get right.

My commitment to zero defects outweighs my commitment to adding features.

#### Time

And I *do* want to add features. There are some features I haven’t seen in other RSS readers — even earlier versions of NetNewsWire — that I want to do.

I think (I hope) they’ll be fun and useful and that you’ll like them. (We’ll see, of course!)

But when I spend time adding some features from an older version of NetNewsWire, I’m not doing the new features that this new world NetNewsWire wants.

#### My Pitch

You might end up disappointed, when NetNewsWire 5.0 ships, that some feature you used in an earlier version of NetNewsWire isn’t there. I totally understand that.

But my pitch is this — or will be (it’s not shipping yet): try an app with zero known defects, where performance is critical, where careful, considered design and simplicity are valued, where there is room for future innovation, where development happens in the open, and see if you like it despite the missing things you wish it had.

You might find you do! And you might not, which is okay — as I mentioned earlier, there are other really good RSS readers, which is a great thing.

PS You can join the Slack group too — just <a href="mailto:brent@ranchero.com">send me email</a>.

PPS I could change my mind in the future about nested folders. Very few decisions are set in stone. But the above is all the things on my mind as I make decisions about things like this.
