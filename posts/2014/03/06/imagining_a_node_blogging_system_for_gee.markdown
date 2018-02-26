@title Imagining a Node Blogging System for Geeks
@pubDate 2014-03-06 10:34:13 -0800
@modDate 2014-03-06 10:35:53 -0800
I’ve written three blogging systems. At UserLand I wrote Manila, which powered editthispage.com and a few other sites way back in the ’90s and early ’00s.

I’ve written two more just for my own use. The first, PHP/MySQL-based, powered this site for seven years. [The second](http://inessential.com/2009/01/30/new_publishing_system_tour_of_my_head), which I still use, is a Ruby static blog generator. I’ve been using it for five years.

I’m a big fan of static sites. In 2011 I wrote [A plea for baked weblogs](http://inessential.com/2011/03/16/a_plea_for_baked_weblogs).

But lately I’ve been writing apps in Node.js, which I like, and I can’t help but wonder how I’d do a blog system. (Yes, I’m aware of [Ghost](https://ghost.org/). It’s probably quite cool, but I’m too impatient to sit through a video, so I don’t know.)

#### Performance

A Node site could out-perform a static site — in theory, at least.

Here’s how I’d do it:

Blog posts would be stored in a calendar-like folder structure on disk. Files would be markdown files. I would need some convention for storing metadata at the top of each file. (My current blog system uses lines starting with a @ character at the top. Maybe MultiMarkdown has something better for this.)

When a page is requested, the server would render it (using Express, Sass, Jade, whatever: standard stuff) and return it. It would also cache the rendered page in memory, in a dictionary — and so the next time the page is requested it would be served from memory.

Apache and Nginx have to hit the file system for each request to a static site. (Correct? I would think, at least, that they have to hit the file system to check if a file has changed before returning from its own cache. I could be wrong.)

But this Node blog could return a rendered page from memory almost all of the time.

The programming for this is so simple. It begs me to try it. (But I’m resisting.)

#### Details

One potential problem is not having enough memory to hold all the cached pages. I doubt that would be an issue since usually it’s just recent posts that get hits. Still, though, you’d have to monitor memory use and adjust as needed.

Another possibility would be to use a Least-Recently-Used cache for the pages. Limit the cache to 20 pages, say, and you’d never have memory issues, but the cache would be a little more expensive to maintain.

Another issue is static assets. Node can deal with those okay, but that’s not what it’s best at. I’d want to put images and similar files on S3 instead. Complicates things a little bit, but with [good tools](https://panic.com/transmit/) and scripts dealing with S3 is fine.

#### Editing

I wouldn’t even bother with an editing UI — instead I’d support the [MetaWeblog API](http://xmlrpc.scripting.com/metaWeblogApi.html) so I could use [MarsEdit](http://www.red-sweater.com/marsedit/). (I sure wish for MarsEdit for iOS. But perhaps there is, at least, something on iOS that works with this API.)

(My static blog system has no editing UI. I write in MarsEdit. I run a small webserver on my machine that implements the MetaWeblog API.)

I’d also want all the posts to be managed by SCM. (Preferably Mercurial, but Git is okay.) On adding or editing a post it would have to commit the changes — I have to assume there’s a Node module for this somewhere. I’d keep local copies of the repository on my machines at home. (Also means I could use my local copies as a staging server, which is nice.)

When a post is edited or added, the cache would potentially (probably) contain one or more pages that need to be re-rendered. Rather than figure out a dependency system, I’d just wipe the entire cache. Editing and adding pages doesn’t happen so often that this would be a problem. (Sometimes the easy way to solve a hard problem is the best answer.)

#### What I like about this

Again, in theory this would be fast. Given a reasonable host and no dumb programming mistakes, it should stand up to a Fireballing at least as well as a static site.

I also like that the system would be portable. In the old days the only really portable thing was static sites — you could zip up a folder and move it somewhere else. Easy. (PHP is portable too, since it’s widely-deployed. But often with a PHP site you have the issue of moving a MySQL database, which is a bit of a pain.)

But these days there are so many different Node hosts (Joyent, Heroku, Azure, Nodejitsu, etc.), and the systems for deploying and running Node are so standardized, that you could consider it very portable. Not as portable as a static site, but portable to an important degree.
