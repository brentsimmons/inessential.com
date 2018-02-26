@title Getting Started with Web Services Using Node and Express (for Cocoa developers)
@pubDate 2013-12-09 21:28:53 -0800
@modDate 2013-12-09 21:32:42 -0800
(See [Getting Started](http://inessential.com/2013/12/09/getting_started_with_node_js_for_cocoa_) if you haven’t already.)

Let’s create an API. I could do something with databases — because that’s probably what you really need — but to keep things simple I’ll leave databases out of it. (I might get to them in a future post.)

#### Don’t Use Node Without It

You need [Express](http://expressjs.com/). There are a ton of packages for Node — it’s a very active community. Express is a web app framework that takes care of a bunch of common things you’d otherwise have to write yourself. (If Node is Foundation, Express is UIKit or AppKit. Roughly.)

Node’s package manager [npm](https://npmjs.org/) makes installing packages easy. I believe it’s installed with Node, so you should already have it.

#### New App

Create a folder called `expressdemo`.

In that folder create a file called `package.json`. It’s like a Cocoa app’s Info.plist — it contains some basic information about your app, including its name, description, version, and a list of Node packages it depends on.

The file should look like this:

<code>{</code><br />
<code>&nbsp;&nbsp;"name": "expressdemo",</code><br />
<code>&nbsp;&nbsp;"description": "Checking out Express",</code><br />
<code>&nbsp;&nbsp;"version": "0.0.1",</code><br />
<code>&nbsp;&nbsp;"private": true,</code><br />
<code>&nbsp;&nbsp;"dependencies": {</code><br />
<code>&nbsp;&nbsp;&nbsp;&nbsp;"express": "3.x"</code><br />
<code>&nbsp;&nbsp;}</code><br />
<code>}</code><br />

If you’re not already in Terminal, open it up and navigate to that folder. Then type:

	npm install

This will read the `package.json` file and install Express and any additional dependencies in a `node_modules` folder inside the `expressdemo` folder. (This keeps your app self-contained. You don’t have to wonder if the system has the right modules installed; you don’t have to wonder if the system has the right *versions* of various modules installed.)

#### Design the API

Our API does two simple things:

1. Returns the current date in a JSON dictionary.

2. Returns the base64-encoded version of a string we pass to it.

We want URLs like this:

<code>/now</code> - returns date<br />
<code>/base64?s=someString</code> - returns base64 of someString

#### Create the Server

Inside the `expressdemo` folder create `server.js` with these lines at the top:

	var express = require('express');
	var http = require('http');
	var app = express();
	app.set('port', process.env.PORT || 1337);

Our app requires the express and http modules, and it creates an app by calling `express()`. It sets the port for listening from an environment variable — but, if that hasn’t been set, it uses 1337.

(Why an environment variable? Because the port shouldn’t be hard-coded. However, it’s useful to have a fallback for when you’re running locally, as we are now.)

Then add the code that starts the server:

<code>http.createServer(app)&shy;.listen(app.get('port'), function() {</code><br />
<code>&nbsp;&nbsp;console.log('Express server listening on port ' + app.get('port'));</code><br />
<code>});</code>

#### Add the API Code

We have two endpoints to respond to. Both use the GET method. Add the function for `/now`.

<code>app.get('/now', function(request, response) {</code><br />
<code>&nbsp;&nbsp;var d = new Date();</code><br />
<code>&nbsp;&nbsp;response.send(200, {date: d});</code><br />
<code>});</code>

Note the `response.send` parameters. The first parameter is the HTTP status code, and the second is the response body. Since the response body is a JavaScript dictionary, the response is returned as JSON. (That’s how easy returning JSON is.)

Then let’s add the /base64 function:

<code>app.get('/base64', function(request, response) {</code><br />
<code>&nbsp;&nbsp;var stringToEncode = request.query.s;</code><br />
<code>&nbsp;&nbsp;var base64EncodedString = new Buffer(stringToEncode, 'utf8').toString('base64');</code><br />
<code>&nbsp;&nbsp;response.send(200, base64EncodedString);</code><br />
<code>});</code>

This time the response body is a string, so it’s returned as itself rather than as JSON.

Note that we got the string to encode via the `request.query` dictionary.

Save `server.js` and run it from Terminal: `node server.js`

#### Testing

Open a new tab in Terminal and try a few things:

	curl -I http://localhost:1337/

The result should be something like this:

	HTTP/1.1 404 Not Found
	X-Powered-By: Express
	Content-Type: text/html
	Date: Tue, 10 Dec 2013 05:07:26 GMT
	Connection: keep-alive

(The -I switch shows just the response headers.)

	curl -I http://localhost:1337/now

The /now endpoint returns the date in a JSON dictionary. The Content-Type header should specify JSON — even though our code didn’t specify that explicitly — and it does:

	HTTP/1.1 200 OK
	X-Powered-By: Express
	Content-Type: application/json; charset=utf-8
	Content-Length: 40
	Date: Tue, 10 Dec 2013 05:09:07 GMT
	Connection: keep-alive

The /base64 endpoint does *not* return JSON, and the Content-Type header should specify text. And it does:

	curl -I 'http://localhost:1337/base64?s=foo'

	HTTP/1.1 200 OK
	X-Powered-By: Express
	Content-Type: text/html; charset=utf-8
	Content-Length: 4
	Date: Tue, 10 Dec 2013 05:10:43 GMT
	Connection: keep-alive

The /now endpoint should actually return JSON with something that looks like a date:

	curl http://localhost:1337/now

	{
	  "date": "2013-12-10T05:13:21.772Z"
	}

The base64 endpoint should return the input string as base64. We know that `foo` encodes as `Zm9v`.

	curl 'http://localhost:1337/base64?s=foo'
	
	Zm9v

It works!

#### Notes

That wasn’t a bunch of code, and you’ve got two endpoints, and one even returns results as JSON. So easy.

Your next step might be to write some unit tests. For that I recommend [Mocha](http://visionmedia.github.io/mocha/).
	
