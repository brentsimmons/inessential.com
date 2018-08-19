@title Now I’m in a Pickle with this Web Stuff
@pubDate 2018-04-16 13:25:06 -0700
@modDate 2018-04-16 13:25:06 -0700
To publish to this blog, I run a little web server on my Mac that implements the [MetaWeblog API](http://xmlrpc.scripting.com/metaWeblogApi.html), which then renders this blog and rsyncs it to the server. (This way I can write using [MarsEdit](https://www.red-sweater.com/marsedit/).)

What I’d rather do: run that little web server on the *actual* server, and do the static-site generation there. That way I can post from my iPhone and iPad, not just from my Mac.

But… here’s where web deployment gets tricky. I’m on an inexpensive shared host plan at DreamHost. The machine is running an older version of Ruby that’s incompatible with my scripts.

I could use [RVM](https://rvm.io/) and [Bundler](https://bundler.io/), I guess, to use the version of Ruby I want to and to install the gems I need. (It’s just a few, but it’s more than zero.)

That is, if I could figure out how to use this stuff and get it installed on the server. Looks like something I could spend weeks doing (remember that my hobby coding is limited to nights and weekends).

Alternately, I could get an inexpensive VPS from one of the various providers and set things up there. That *might* be easier — maybe I could skip RVM and Bundler and just install the things I want to use in the old-fashioned way.

But then I have to deal with a bunch of other things myself, including setting up Apache or Nginx. All the things DreamHost does for me automatically I’ll have to handle myself. That doesn’t sound like fun *at all*.

I totally don’t know what to do. It’s not my plan to become a Ruby deployment expert or to be on the hook for running a server all the time. I’ve done *way* too much of that kind of thing for one lifetime already, and I’ve mostly been glad to be out of it.

What surprises me is that in 2018 it still requires so much work just to get a CGI script running on a server. It should be easier.
