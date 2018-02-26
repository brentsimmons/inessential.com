@title How Not to Crash #5: Threading, part 2
@pubDate 2015-05-26 11:23:43 -0700
@modDate 2015-05-26 11:26:20 -0700
My <a href="http://inessential.com/2015/05/22/how_not_to_crash_4_threading">previous post about threading</a> left open the question of how code running outside the main thread communicates — safely — back to the main thread.

The object creating the background task handles the result of the task. This is a hard rule.

Usually the object creating the task is an object that lasts for the lifetime of the app. An example might be an image cache — the cache may get emptied during the lifetime of the app, but the cache object lasts for the duration.

Another example is something like Vesper’s VSAccount object. There’s *always* a single VSAccount instance. The user may or may not have a server account. The user may change which server account they’re using. But there’s a single VSAccount object which lasts for the lifetime of the app.

(Note: obviously, an app that manages multiple accounts would do things differently. But Vesper manages at most one server account, so this works perfectly well. In Vesper’s case, multiple accounts falls under the YAGNI rule.)

The VSAccount object is responsible for sending http requests to the server and handling the result. It turns JSON into intermediate objects on a background queue.

It calls the JSON processor with NSData-to-process and a callback block. When the processor is finished, it calls that block on the main thread:

<code>if (callback) {</code><br />
<code>&nbsp;&nbsp;dispatch\_async(dispatch\_get\_main\_queue(), ^{</code><br />
<code>&nbsp;&nbsp;&nbsp;&nbsp;callback(parsedObjects)</code><br />
<code>&nbsp;&nbsp;});</code><br />
<code>}</code>

This is such a common pattern for me — calling a block that takes one parameter on the main queue — that I have a common function for it. The JSON processor really just does something like this:

<code>BSCallBlockWithParameter(callback, parsedObjects);</code>

BSCallBlockWithParameter looks something like this:

<code>if (!callback)</code><br />
<code>&nbsp;&nbsp;return;</code><br />
<code>}</code><br />
<code>dispatch\_async(dispatch\_get\_main\_queue(), ^{</code><br />
<code>&nbsp;&nbsp;callback(parsedObjects);</code><br />
<code>});</code>

I use this all the time. Super handy.

#### The key to making this work

I don’t ever want to worry that the object that created the background task might go away, so I create background tasks only from objects that last the lifetime of the app.

You don’t want to get into the situation where an object that creates a background task goes away (or is torn-down partly or completely) before that task is finished and calls back. It’s a potentially complex subject, and I don’t even want to think about it. (I *hate* the weak-self dance, for starters.)

And that’s exactly the mindset you need when writing code that doesn’t crash: if something is complex, then it’s error-prone. Find a way to make it drop-dead simple.

(You could figure out a complex thing and prove that it’s correct — but will you have doubts later and feel the need to audit that code? Will it break if you breathe on it wrong? Or if someone else touches it?)

So I do the simple thing: use objects that won’t get deallocated.

But there’s an escape hatch worth remembering: a callback block can call class methods and C functions safely. Instance methods are unsafe if the instance disappears — but class methods and C functions are conceptually safe to call.

I don’t use this knowledge very often, but I have found it useful from time to time. Use sparingly if at all.
