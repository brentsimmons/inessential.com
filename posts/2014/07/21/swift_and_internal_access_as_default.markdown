@title Swift and Internal Access as Default
@pubDate 2014-07-21 13:15:36 -0700
@modDate 2014-07-21 13:15:36 -0700
So if internal access is the default, and I don’t want to use it (or want to use it exceedingly sparingly), what do I do?

I can think of a few options.

* Just pay attention. By convention treat internal as private, and pretend that other objects can only see what’s public. The compiler won’t enforce this, but it’s the kind of convention that’s easily enforced manually if it’s habit.

* Actually mark every damn thing as either public or private. Just don’t ever use the default. That’s a pain, but also the kind of thing that’s not that hard if it’s habit.

* Modularize.

The last one intrigues me. My app could be broken up into modules — <a href="https://github.com/quartermaster/QSKit">Q Branch Standard Kit</a>, <a href="https://github.com/quartermaster/DB5">DB5</a>, data layer, syncing, images/attachments rendering and storage, and user interface.

In that case, I’d be less bugged about objects presenting a larger API, since the objects that could see that expanded API are only other objects in the same module.

I do have a natural bent toward modularizing. I’ve always liked splitting things into frameworks. And the tea leaves clearly spell out Way of the Future for this approach.

But I have two objections, one practical and one theoretical.

The practical one is that I’m still shipping an app for iOS 7, which doesn’t support embedded frameworks. (Or, not exactly.) That problem will take care of itself after a while — but still, it means that right now I’d have to start an iOS 8 branch just for frameworks, which leads down the road to merge debt. Merge debt’s a killer.

The theoretical one is the same problem I expressed previously: where I used to think about public vs. private, now I have to think about public vs. internal vs. private, and I’m not sure that that additional complexity is good for me. The discipline of public vs. private, along with the drive to reduce what’s-public down to the barest minimum, has been good for my designs. It suits my brain — which is more experienced than it is clever — quite well.

There’s an argument that frameworks really need this, that objects need to expose some bits to their neighboring objects that they don’t expose to the world. I bet that that’s how many frameworks have been written. But I also bet that that’s *not* how I’d do it.

But I could be wrong, and I could be missing out, and maybe I’m just being a stick in the mud.
