@title Still looking for a version control system
@pubDate Sat Mar 07 12:38:19 -0800 2009
@modDate Sat Mar 07 12:38:19 -0800 2009
A few years ago I switched from CVS (ugh) to <a href="http://subversion.tigris.org/">Subversion</a>. I’ve been largely happy with it. (As recently as last summer I had <a href="https://explore.twitter.com/brentsimmons/statuses/843548911">no plans to switch</a>.)

I use version control just for me: I’m not collaborating on a source code level with other people.

I have two machines: a desktop, my main development machine; and a laptop, where I like to work sometimes or where I work when on the road.

(The benefits of version control for the solo developer, even one using just one machine, are well-known and I won’t rehash them.)

#### How I work

When I feel like working on my laptop, I make sure everything is committed on my desktop, then do an update or pull to get my laptop up-to-date. Then I work on my laptop for a while, then commit back to the desktop.

#### Trying Git

A little over a month ago I switched to <a href="http://git-scm.com/">Git</a> for my fastest-moving project. There’s a lot to like about Git.

But what I don’t like is that it’s <em>more</em> work for me than Subversion.

When I’m finished working on my laptop and I commit my changes, they’re not available on my desktop. I have to take the extra step of pushing the changes.

And then, back at my desktop, I have to figure out how to update the working copy to reflect the changes from my laptop. Which for some reason I have to figure out anew every time: I can’t remember it and I haven’t made a note of it. (Because, every time, I’m dumbly convinced that <em>this</em> time I’ve remembered it.)

To make matters worse, I’m really not sure if I’m doing it right. And <em>uncertainty</em> regarding your version control system is a bad, bad, evil thing.

I fully admit that this stuff is figure-out-able, and I suspect that any Git users reading this are wondering if I’m bright enough to be a software developer, or even to tie my shoes reliably.

But it is, still, verifiably <em>more work</em>. That’s just the nature of distributed version control in cases like this.

#### Tool philosophy

My philosophy is that programmers should spend most of their time in their text editor. It’s where you write code.

You have to spend time compiling and building, of course. Looking at the bug tracker. Gathering feedback. Designing. Debugging. Thinking. Testing. And you have to spend some time with version control.

But you’ve got to write code, mostly. Everything else is marginal. Important, but not the central activity.

People talk about how wonderful are features like re-writing history — and I read that stuff and think, “Wow, Git’s really cool and powerful.” But then I know it could suck me in and take away time from <em>real</em> work. It’s <em>already</em> more work — <em>for me</em> — than when using Subversion.

Ideally, my version control system does two things:

1. Makes it easy to use two different machines.

2. Saves my bacon.

Bacon-saving is, obviously, the most important of the two, but it’s a rare thing. In day-to-day use, using it to sync two machines is the far more common use.

Something simple and easy-to-use that did both would be <em>great</em>. As fun as it is, I don’t really want to let myself futz with my version control system: <em>I want to write code</em>.

(I don’t want to build my own PC, either. Or endlessly tweak a Linux installation. Or comparison-shop for subwoofers. Or use Office.)  

#### My problem with Subversion

When I leave the house with my laptop and want to do some work, I can’t get to my Subversion repository, since it’s at home on my desktop.

So that leaves me coding without a net. Which I hate.

It hasn’t cost me any bacon yet, but I worry about bacon loss — which is just plain not a good feeling.

#### Bazaar?

I might try out <a href="http://bazaar-vcs.org/">Bazaar</a>. I did some reading about it, and apparently it can be used, Subversion-like, with a central repository. In that configuration it doesn’t work like a distributed version control system.

But it also has <em>bind</em> and <em>unbind</em> commands, which would allow me to go local when I’m traveling with my laptop, then go centralized when I get back home.

#### No conclusion

If I switch one project over to Bazaar, I’ll still be using Git and Subversion on others.

It may be that I’ll figure out a good Git workflow that works for me. There are things Git does better than Subversion, after all. (They just haven’t become important to me yet.)

Or I’ll just go back to Subversion, but use Git when traveling (and check back into Subversion on return). Or maybe Bazaar is really the system I’ve been waiting for, and I’ll love it.

I don’t know. Still looking.
