@title How Much, or How Little, I Use Interface Builder These Days
@pubDate Wed Mar 06 15:35:40 -0800 2013
@modDate Wed Mar 06 15:56:26 -0800 2013
Yesterday I tried using Cocoa auto layout in my latest project. I’d tried it before — and gotten quickly frustrated.

The difference this time is that I didn’t use Interface Builder. I set up the constraints in code, using <a href="https://developer.apple.com/library/mac/#documentation/UserExperience/Conceptual/AutolayoutPG/Articles/formatLanguage.html#//apple_ref/doc/uid/TP40010853-CH3-SW1">ASCII art layout strings</a>.

And it worked quite nicely.

#### CGWrecked

I’m an accomplished CGRect-slinger. I’ve been doing layout in <code>layoutSubviews</code> and the Mac equivalent for more than a decade.

I can do it in my sleep. Which is good, because writing layout code makes me sleepy. It’s one of the most tedious bits of programming — not at all interesting or fun.

The thing about CGRect-slinging is that you have two steps:

1. Figure out the rules.
2. Translate the rules into code that sets the frames of your views.

I like auto layout because it’s more like one-and-a-half steps: figure out the rules and then type up the rules.

You still have to translate, but it’s a shorter distance. Like going from English to French — instead of going from English to the tentacle-speech of Alpha Centaurans. (Those cats have more than 49,000 words for methane snow.)

#### Punching and Cursing

The problem with IB and auto layout is that IB adds constraints as you’re working. It won’t let you have ambiguous constraints.

The thing is, they’re bound to be ambiguous as you’re working on them. So IB will get in your way, and you end up fighting it and calling it dirty names you didn’t know you knew. Or at least that’s what I do.

#### Keeping the Dream of the ’90s Alive

I always thought that Interface Builder was the product of a beautiful idea: coders would write code, and designers would create interfaces using a drag-and-drop design app.

But — in my my experience, and based on everything I’ve heard — designers use Photoshop, <a href="http://www.flyingmeat.com/acorn/">Acorn</a>, Keynote, <a href="http://www.omnigroup.com/products/omnigraffle/">OmniGraffle</a>, and so on instead. IB shows you at best an approximation of what the app will look like — while designers want to see <em>exactly</em> what the app will look like.

Sure, a designer could work in an image editor and <em>then</em> work in Interface Builder. But it’s a rare designer who does. Instead they create mockups and movies and let the programmer do the Xcode work. (Yes, there are designers who code, even. I know. But this is still generally true.)

I had thought, when Apple moved IB into Xcode, that it was tacitly acknowledging this. But then storyboards made me wonder if Apple is still keeping the beautiful dream alive.

#### Life in Programmer-Land

Despite the dream, IB is very much a part of programmer-land. It’s not designer-land.

So the question becomes: as a programmer, do you find it useful?

I’ve found that I use it less and less. I use it almost solely for very static screens.

It may make it easier to set things up at first — but that’s like using <a href="http://en.memory-alpha.org/wiki/Protomatter">protomatter in the initial matrix</a>, which history tells us is a poor call. (It’s a shortcut that leads invariably to pain.)

Here are some of the problems I run into when using IB:

• Navigating back and forth between code and a xib file is a pain, even on my big screen. (To go through all that just to change a background color feels ridiculous.)

• Diffing versions of a .m file is nice. Diffing versions of a xib file is terrible.

• Pointing-and-clicking and dragging-and-dropping is *not* how a programmer gets through their day. It’s an unwelcome context switch.

Any one of those would be enough: all three thoroughly convince me to stay away from IB for all but the rarest cases.

And the fourth reason I added just yesterday is that dealing with auto layout in IB is not worth the hassle — not when it’s so much easier done in code.

#### But more code is more code, right?

Eschewing IB does mean writing code to create and configure your views. And that is, no doubt about it, more code.

But I look at it this way: it’s fewer entities. For each line of code there would have been a corresponding thing in IB.

And fixing a thing in code is simpler than fixing it in IB — because as programmers we’re optimized for code-writing.

Want to fix a color or change the position of a view? I like doing it the way I solve every other problem: I code it.
