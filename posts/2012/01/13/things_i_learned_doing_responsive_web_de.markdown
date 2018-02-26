@title Things I Learned Doing Responsive Web Design
@pubDate Fri Jan 13 20:09:26 -0800 2012
@modDate Fri Jan 13 20:11:51 -0800 2012
It looks like the web is being born again, again.

Here are some things I’ve noticed about the web:

1. Designers have realized the need to design for mobile devices and tablets, and they’ve come up with <a href="http://www.alistapart.com/articles/responsive-web-design/">responsive design</a> rather than doing special mobile versions.
2. CSS3 and HTML5 are gaining support, and they make possible some things that were difficult or practically impossible before.
3. There’s an explosion of technologies: <a href="http://lesscss.org/">LESS</a>, <a href="http://sass-lang.com/">Sass</a>, <a href="http://compass-style.org/">Compass</a>, and <a href="http://twitter.github.com/bootstrap/">Bootstrap</a> for CSS; <a href="http://jashkenas.github.com/coffee-script/">CoffeeScript</a> for JavaScript; app frameworks such as <a href="http://documentcloud.github.com/backbone/">Backbone.js</a> and <a href="http://thinkvitamin.com/code/javascript/ember-js-a-more-lightweight-sproutcore/">Ember.js</a>; server-side technologies such as <a href="http://nodejs.org/">Node.js</a>, <a href="http://www.sinatrarb.com/">Sinatra</a>, and <a href="http://en.wikipedia.org/wiki/Nginx">nginx</a>; and interesting new databases such <a href="http://code.google.com/p/leveldb/">LevelDB</a> and <a href="http://couchdb.apache.org/">CouchDB</a>. And more — <em>plenty</em> more.
4. Web fonts are finally practical: see <a href="https://typekit.com/">TypeKit</a>, <a href="http://emigre.com/WebFonts">Emigre Web Fonts</a>, and <a href="http://www.google.com/webfonts">Google Web Fonts</a>.
4. Flash is finally losing ground, and developers are replacing it with standards-based technology.
4. There’s a renewed interest in design of all kinds — very much including web design. See <a href="http://dribbble.com/">Dribbble</a> and <a href="http://www.uiparade.com/">Ui Parade</a>. Native mobile app design ideas are coming to web design, and designers are experimenting.
4. Deploying applications is cheaper than ever, thanks to <a href="http://en.wikipedia.org/wiki/Virtualization">virtualization</a> and to <a href="http://aws.amazon.com/">Amazon Web Services</a>, <a href="http://www.heroku.com/">Heroku</a>, <a href="http://www.windowsazure.com/en-us/">Azure</a>, <a href="http://www.engineyard.com/">Engine Yard</a>, and others.
4. Collaboration has gotten easier due to <a href="http://git-scm.com/">Git</a> and <a href="http://mercurial.selenic.com/">Mercurial</a> — and perhaps even more due to <a href="https://github.com/">GitHub</a> and <a href="https://bitbucket.org/">Bitbucket</a>.
4. While the giant companies are busy rediscovering the America OnLine model of walled gardens, while Congress is debating the <a href="http://en.wikipedia.org/wiki/Stop_Online_Piracy_Act">Stop Online Piracy Act</a>, developers are remembering the web as the open garden of free speech. And they don’t want to lose it.

I haven’t done serious web work — HTML web work, that is — since I last worked on <a href="http://en.wikipedia.org/wiki/UserLand_Software#Manila">Manila</a> 10 years ago.

I’ve done some small things — the system that generates this blog, for instance — but I haven’t had the chance to use almost any of the newer web technology. I’ve never written a <a href="http://rubyonrails.org/">Rails</a> app, used <a href="http://jquery.com/">JQuery</a>, or deployed to a virtual server.

So when I had the chance to re-do the websites for our company and main product, I was excited — because it meant I could try some of the new technologies and learn some things.

#### The plan: re-do four sites

I wanted to re-do SepiaLabs.com and Glassboard.com — their home pages and blogs. That’s two sites, but in practice it was four sites.

I did them in this order:

* <a href="http://sepialabs.com/blog/">SepiaLabs.com blog</a>
* <a href="http://sepialabs.com/">SepiaLabs.com home page</a>
* <a href="http://glassboard.com/">Glassboard home page</a>
* <a href="http://glassboard.com/blog/">Glassboard blog</a>

I had two main goals:

1. Make them look at least credible.
2. Make them work on tablets and mobile devices.

I don’t claim these as exemplars of design, and there are bugs and nits to fix — there’s <em>plenty</em> of room for improvement. Tons of room.

I’ll talk about #2 — responsive web design — and what I learned.

#### Breakpoints

Responsive design works because of the combination of CSS layout and CSS media-queries. You can change the layout for different sizes.

When I first started, I created two breakpoints (where the layout changes): one for iPad-sized screens and one for phone-sized screens. It seemed logical.

Later on I figured out a better way: create breakpoints when the layout breaks.

I just shrank the width of my browser window until the design broke in some way, then I dealt with it, either by changing things or by creating a breakpoint and changing the layout at that point.

This made more sense because I was working with the design rather than thinking about specific devices.

#### Layout

It was kind of like working with toothpaste.

When the layout broke and I created a breakpoint, I worked from the top down to fix the layout. The more narrow the screen, the more the layout became vertical, and the more often I relied on centering to make things work. I also hid things (via <code>display: none</code>) that were nice at bigger sizes but that weren’t needed at smaller sizes.

That’s not the most sophisticated approach, but, given the time constraints and my goals, it worked.

#### Why not design for mobile first?

As I was finishing the sites I read some advice on the web: design for mobile first, then build up to the desktop size.

I like this advice because it forces you to think about what’s utterly necessary from the start, and it makes sure the mobile size is not an afterthought or something done in a hurry when the project is due.

That’s not what I did, but I think I’ll try it next time (whenever that may be).

#### CSS Transforms

Sometimes I needed to move something from where it would naturally be to somewhere nearby. Sometimes the traditional way of doing it would make for bad code: divs-within-divs-within-divs, or worse.

One way to move something a little bit is to use <code>translate</code>, <code>translateX</code>, or <code>translateY</code>. Simple.

I kind of think of this as a bit of a cheat — certainly something to be used sparingly. But it worked.

#### Tools

I started by doing CSS by hand, just me and a text editor. I got about halfway through before I switched to Sass and Compass.

Sass is wonderful. (I’m sure I’d like LESS no less.) Just having variables alone would be enough for me to love Sass, but it has a bunch more (functions!) besides.

The way it works is that you launch a command-line script that watches for changes in your .scss file (the file that you edit). When it changes, it compiles a .css file. It happened so quickly that I never noticed the compile time.

#### JavaScript

Though the sites have some JavaScript, none of it is used to make the sites work at different screen sizes. I didn’t think it would be necessary, and it turned out I was right. (Using JavaScript for this would make the sites harder to maintain, I reasoned.)

#### Testing

Testing on my desktop was easy: I used Safari, Chrome, and Firefox. I also then uploaded the sites to a staging server and tested with IE 9 on Vista and Chromium on Ubuntu (via VMWare) and tested with an iPad and an iPhone. Other folks in the company tested with other browsers and with Android devices.

But testing was absolutely necessary. Though adoption of CSS3 has progressed, this is not quite standards-based Eden.

#### Version control

I created a local Mercurial repository whenever I started a project. I have not yet taken this all the way. I should have a repository that other folks at the company can access, and I should have a deploy script for staging and live servers.

This is made somewhat complicated by the blogs: they’re WordPress blogs, and I don’t know if changing a theme is scriptable. (Maybe it is. I haven’t looked yet.)

#### What have I not learned?

I’ve dipped my toes in: I’m a novice. At this point in learning new technology I try to get a rough idea of the size and shape of everything I haven’t learned yet. I also assume that I’ll look back to now and smack my forehead.

But there’s an important thing I did learn: I learned that this work is <em>fun</em>.

I was reminded of how the Cocoa world felt in 2002 — those days felt like early days again. There was so much excitement for what we could make and what would come next.

And now it feels like that for the web. Again.
