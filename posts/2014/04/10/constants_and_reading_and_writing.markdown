@title Constants and Reading and Writing
@pubDate 2014-04-10 12:16:22 -0700
@modDate 2014-04-10 12:21:23 -0700
It’s common wisdom — and *almost* always correct — that it’s better to use constants than literals. As in <code>return VSSidebarWidthMaximum</code> instead of <code>return 256.0f</code>. I agree completely with that wisdom.

But there are two particular (and similar) cases where I disagree. Which is better?

<code>response.send(200, someStuff);</code>

…or…

<code>response.send(statusCodes.OK, someStuff);</code>

For me the first one is far better. By now the HTTP response codes are wired deep into my brain, and so the 200 literal is much easier to write and read than any constant.

Another example:

<code>[request setHTTPMethod:@"POST"];</code>

…or…

<code>[request setHTTPMethod:VSHTTPMethodPost];</code>

The first one wins. Yes, there is the possibility that I’ll mis-type it, and of course the compiler won’t tell me. But that trade-off is totally worth it, because now I can see instantly that it’s a POST method request. My brain doesn’t need to translate. (The odds of my mis-typing `@"POST"` and not noticing it are ridiculously small.)
