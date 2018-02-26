@title Mobile Services’s HTTP API
@pubDate 2014-06-17 09:51:13 -0700
@modDate 2014-06-17 09:51:13 -0700
I got an email this morning asking me about using Azure Mobile Services from the Mac.

Here’s the thing: Mobile Services provides an [open source SDK](https://github.com/Azure/azure-mobile-services) with iOS support but without Mac support.

Given that the name is *Mobile* Services that’s not a complete surprise. However, it’s no stretch to imagine that you’d want to use these services on a Mac too, as we do with Vesper.

I haven’t spent much time with the framework, but it appears to be good. It includes some very nice things, such as support for querying the server using NSPredicate.

Instead — because I knew we’d be doing a Mac version — I wrote my own code for talking to the server. It was ridiculously easy.

Mobile Services is a hosted Node.js service with a bunch of yummy sugar on top. The thing to know is that that sugar doesn’t get in the way of calling web services the same way you’re used to.

#### How to Call a Mobile Services Endpoint

Most of the time, if not all the time, you’ll be passing JSON to an endpoint and getting JSON back.

So you have to do the right things with the JSON, just as with any other server: serialize it to NSData, setHTTPBody, and set the Content-Type header to application/json. And you’ll have to turn the response data into a JSON object and then do the right things with that JSON.

For any endpoint that requires the application key (which is any level except for the “Everyone” level), you have to add your public app key to your request headers.

It’s as simple as this:

<code>[request setValue:&#8203;@"your\_public\_app\_key" forHTTPHeaderField:&#8203;@"x-zumo-application"];</code>

(I’ve never asked, but I assume *zumo* is short for aZUre MObile.)

For any endpoint that requires user authentication, you need to add the user’s JWT authentication token that the server provides on login:

<code>[request setValue:&#8203;authentication&#8203;Token forHTTPHeaderField:&#8203;@"x-zumo-auth"];</code>

Getting the URL of an endpoint is pretty simple. For the table-based calls, I think the prefix is “table.” (I’m 99% sure.)

We use custom API exclusively with Vesper, and the prefix is “api.”

So, to construct a URL, take your service name, add the prefix, then add the name of the endpoint. As in: <code>https://coolservice.&#8203;azure-mobile.net/&#8203;api/&#8203;myendpoint</code>.

(Because it’s a Node service that uses the Express router, you can create longer URLs — such as /api/myendpoint/foo/bar?a=b — but you don’t have to. API design is up to you.)

Now: the one thing that could be a challenge with a Mac version is if you’re using Twitter or Facebook as identity provider. We’re not doing that — we wrote our own accounts system, using [this code as our starting point](http://www.thejoyofcode.com/Exploring_custom_identity_in_Mobile_Services_Day_12_.aspx) — because we found that people get nervous that Twitter or Facebook might have access to their data. (They don’t, but that’s a hard thing to explain.)

So, if you’re using Twitter/Facebook login, you’ll have to figure that out — but you have the iOS Mobile Services SDK to guide you. It’s work, but there’s nothing magical about it: it should be figure-out-able.
