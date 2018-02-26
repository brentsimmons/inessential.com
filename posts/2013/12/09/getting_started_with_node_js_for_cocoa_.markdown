@title Getting Started with Node.js (for Cocoa developers)
@pubDate 2013-12-09 14:30:12 -0800
@modDate 2013-12-09 14:49:01 -0800
There are three parts to your iOS or Mac app: design, implementation, and back-end.

Design is what it does, how it works, and what it looks like. Implementation is what you do in Xcode. The back-end is — well, it’s, hrrmmm, something other people do? Or something [we just ship without](http://vesperapp.co/)?

#### What Tim Said

Here’s Omni Group CTO Tim Wood talking about syncing: [Own the Wheel](https://twitter.com/tjw/status/289230416064425984). I think this applies to more than just syncing — it applies to whatever back-end services your app needs, even if you’re a solo developer or part of a small shop.

(Unless, of course, you’re writing an app whose reason-for-being is to act as a client for somebody else’s service. Given the experience of Twitter and Google Reader client developers, you might consider this decision carefully.)

There are two pieces of good news. One is that learning this stuff isn’t that hard. The other is that it’s really *fun*.

#### Node.js

There are lots of web app frameworks. They don’t all do the same things: you can’t compare apples to apples. [Node](http://nodejs.org/) by itself isn’t even really an app framework — it’s a *server* framework.

I like it because it’s [fast](https://www.google.com/search?client=safari&rls=en&q=node+performance&ie=UTF-8&oe=UTF-8), lightweight, and has wide support. You write code in JavaScript — and, while I don’t love JavaScript, I do like it (to my surprise), and it means one language for server-side and in-browser code.

Node will be instantly familiar to Cocoa developers. It has a main thread run loop. I/O is non-blocking and calls back to your scripts on the main thread. JavaScript has closures (blocks, in our world) which make all this easy.

#### Install Node

The [Node.js downloads page](http://nodejs.org/download/) has an installer for Macs. Get it and install it.

#### Write a Server

Open up a text editor and add the following code.

<code>var http = require('http');</code>

This is kind of like an `#import` statement. It brings in the http module and assigns it to a variable. (In JavaScript, always declare your variables with `var`. Always.)

Then create a server. This server does one simple thing — it returns the name of your favorite color.

<code>var counter = 0;</code><br /></br />
<code>var server = http.createServer(function(request, response) {</code><br /></br />
<code>&nbsp;&nbsp;response.writeHead(200, {'Content-Type': 'text/plain'});</code></br /></br />
<code>&nbsp;&nbsp;var color = 'blue';</code></br />
<code>&nbsp;&nbsp;if (counter % 2 === 1) {</code></br />
<code>&nbsp;&nbsp;&nbsp;&nbsp;color = 'no, green';</code></br />
<code>&nbsp;&nbsp;}</code></br /></br />
<code>&nbsp;&nbsp;response.end(color);</code></br />
<code>&nbsp;&nbsp;counter++;</code></br />
<code>});</code>

Note the `function(request, response)…` part — that’s your callback. The server calls it on the main thread when there’s a new request.

Then start the server:

	server.listen(1337);

This tells the server you just created to listen on a particular port.

Save the file as server.js.

(Also note that `counter` variable. There’s nothing special about it — except that there are no locks around it. There’s no need, since `counter` is always referenced on the main thread.)

#### Run It

You’ve written a working web service. Now you just need to run it.

In Terminal, from the same folder where you saved server.js, do this:

	node server.js

It’s running. (You can quit it with ctrl-C any time later.)

#### Test It

You can open it in your browser: [http://localhost:1337/](http://localhost:1337/)

Reload the page to see the response change.

Or on the command line (cmd-T to create a new tab in Terminal):

	curl http://localhost:1337/

It works!

#### Notes

Node has a REPL. I use this constantly as I’m learning JavaScript syntax and various APIs. On the command line, just type `node` and hit return. You’ll get the Node > prompt.

Then you can do things like this:

	> var x = {}
	undefined
	> x.foo = 'bar'
	'bar'
	> x
	{ foo: 'bar' }
	> var y = encodeURIComponent('this is a string')
	undefined
	> y
	'this%20is%20a%20string'

The parts after the > are where you type. The result appears below. (Type ctrl-D to quit.)

You can even [write shell scripts using Node](http://www.2ality.com/2011/12/nodejs-shell-scripting.html).

While Node is cool, it’s not much of a web *app* framework. For that you need [Express](http://expressjs.com/). I’ll write about Express in a follow-up. (I’ll also write about npm, the Node package manager.)

Though it’s not Node-specific, [The Twelve-Factor App](http://12factor.net/) is worth reading for a high-level view of how web apps are built these days. (It’s a website/essay. Not that long. *Highly* recommended.)

You might think you need to buy a server, or rent a virtual server, to run Node — but that’s actually not true. Plenty of places offer Node hosting, where you deploy your app (via Git, usually) to their server, and you don’t have to worry about security patches and all that stuff. See [Heroku](https://devcenter.heroku.com/articles/getting-started-with-nodejs), [Azure](http://www.windowsazure.com/en-us/develop/nodejs/), [Joyent](http://www.joyent.com/technology/nodejs), [Nodejitsu](https://www.nodejitsu.com/), and others. (I’ve got nothing against buying or renting servers for other reasons. I’m a fan of [Macminicolo.net](http://macminicolo.net/), for instance.)

Also check out [Felix’s Style Guide](https://github.com/felixge/node-style-guide).
