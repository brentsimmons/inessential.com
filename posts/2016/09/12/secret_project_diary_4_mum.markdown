@title Secret Project Diary #4: MUM
@pubDate 2016-09-12 13:53:39 -0700
@modDate 2016-09-12 13:54:13 -0700
Some random notes on my secret project Mac app…

<p style="text-align:center">* * *</p>

It’s very close to what I call the Minimally Usable Milestone (MUM). That doesn’t mean all the features are all there — or even that they’re all designed — but that you could use the app for its main purpose, if you don’t mind all the unfinished parts.

This is pretty exciting for me. What this means is that the app has good bones, and now it’s a matter of implementing commands, doing some side windows, that kind of thing. It’s still a ton of work, but it’s rewarding in a specific way: every bit of progress is something I can see and use. Up until now it’s mostly been programming-by-faith.

The app has taken a long time to get to this point for a few reasons. One is that I was working on two apps at the same time. I realized that it wasn’t realistic to do two — so I picked the one I wanted to do the most.

Another is that I work in bits and pieces — 15 minutes here and there, and when I’m lucky a few hours in a row on the weekend. As long as the work is steady I don’t lose context — and even 15 minutes a day adds up after a while (especially as you consider that some of the work is thinking work that happens in the shower, on the bus, and so on).

A third is that I have the luxury of shipping whenever, which means my process goes like this: write the code to understand the problem, then write it again now that I understand it. It’s not fast, but I do it this way because it’s super-important to me that I don’t have to do major surgery later. The bones, the foundation of the app, should need only minimal attention after 1.0.

<p style="text-align:center">* * *</p>

I don’t know when the beta will be. I don’t know if it will be public or not. But it won’t go into beta until 1) there are no known crashing bugs, 2) there are no known bugs, and 3) it’s fast. (Of those three, the hard one is really #2.)

However, there will be testers who see it <a href="http://inessential.com/2016/08/27/on_beta_testing">before it hits beta</a>. I like early feedback. But even that is still a ways away.

<p style="text-align:center">* * *</p>

All of the code at the app level is in Swift. There are about 10 frameworks (modules) that the app uses: some could conceivably be used in other apps, and others are app-specific. The oldest of these still has a bunch of Objective-C code, while newer modules are in Swift. It’s rare that I write a new line of Objective-C.

I like not just writing modular code but actually enforcing that by using actual modules. Though some modules may depend on lower-level modules, they’re each otherwise self-contained, with their own tests and so on. I like to be able to focus: I select the module in that popup in the Xcode toolbar, and then just work on it and forget about everything else.

<p style="text-align:center">* * *</p>

I’ve found a simple organization pattern that I like for my Swift code.

* Properties at the top.
* Init methods
* Public or internal methods.
* Then a `private extension`. The public/internal methods can see into the extension, but nothing else can. (This way I never have to mark an individual func as private.)

I also make heavy use of <code>// MARK: Whatever</code> for organization.

I do *not* make separate extensions for protocol conformance methods. I tried it and it felt too busy. Instead I just have public/internal and then the private extension.

I also mark things as `final` all the damn time. Subclasses are the devil’s classes. I’m a big fan of protocol-oriented-programming. 

And: my methods tend to be small. This is probably a function of my available time — I break things into smaller chunks, because I only have time for a small chunk. It’s probably also a function of my having to enlarge my font size in Xcode. Something in my brain responds to the actual physical on-screen size and not the number of lines of code.

<p style="text-align:center">* * *</p>

I keep the app to-do list in <a href="https://www.omnigroup.com/omnioutliner">OmniOutliner</a> (which I work on at my day job), since app to-do lists are hierarchical. I’ve been using an outliner for this purpose since the ’90s, and OmniOutliner specifically for probably more than ten years. I have no idea if anybody else does this, but for me it works great.

I will use a bug tracker later, of course, but for now there’s no need. A big flat list would be unwieldy at this point. I need to see the structure of what needs to be done, and I need to expand and collapse so I can focus. (Obviously OmniFocus might also be good for this purpose.)

I use OmniOutliner very simply. Hide the toolbar. Hide the inspector. One column only. No status checkbox — I just delete lines as they’re completed (because otherwise they add noise).

<p style="text-align:center">* * *</p>

Next up on the Secret Project Diary — I’m not sure when — I plan to write about the app I’m not doing. The one that got away.
