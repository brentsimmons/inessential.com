@title NSURLSessionData&shy;Delegate and objc/runtime.h
@pubDate Sat Oct 12 14:48:50 -0700 2013
@modDate Thu Oct 17 11:35:39 -0700 2013
While checking out the new `NSURLSession` system, I was surprised to find that the session, and not the individual tasks, take a delegate.

One of the delegate methods is this:

<code>- (void)URLSession:&#8203;(NSURLSession \*)&#8203;session dataTask:&#8203;(NSURLSessionDataTask \*)dataTask didReceiveData:&#8203;(NSData \*)data;</code>

#### Example

Say you’re writing an RSS reader or podcast client. The app downloads a bunch of feeds, and passes data to a streaming XML parser, one per download, as it arrives.

How do you know which feed is associated with which task?

If each <code>NSURLSession&#8203;DataTask</code> had its own delegate, you could give that delegate a feed property. Easy. (That’s how you’d have done it with the old <code>NSURL&#8203;Connection</code> system.)

I can think of a few options:

• Overload `taskDescription` — give it the URL of the feed, for instance. I don’t like this, though, because that’s really supposed to be, according to the headers, a descriptive label for the task. Not a data container.

• Look at `originalRequest` and look up the feed object based on the URL. Feels a little fragile (though it shouldn’t be) and it’s kind of a pain.

• Subclass <code>NSURLSession&#8203;DataTask</code> and add a feed property. I don’t see a way to do that, though, since the <code>NSURL&#8203;Session</code> creates data tasks.

• Maintain some kind of map — using an `NSMapTable` or <code>NSMutable&#8203;Dictionary</code> — that maps data tasks to feeds. Do-able, but ugly. Not particularly object-oriented.

• Hack it.

#### The Hack

Rule of thumb: if <code>#import &lt;objc/runtime.h&gt;</code> appears anywhere in your production code, you’re probably making a mistake.

It’s fun to play with the runtime, and you absolutely should — it’s part of becoming a good Cocoa developer. But you shouldn’t ship those hacks.

This may be a case where it’s warranted, though.

I may change my mind, but right now I’m thinking that using associated objects is the way to go. Associated objects let you attach any data to any object.

On creating the data task, I’d have code like this:

<code>static const char *associated\_feed = @"associated\_feed";</code><br />
<code>objc\_setAssociatedObject&#8203;(dataTask, associated\_feed, feed, OBJC\_ASSOCIATION\_RETAIN);</code>

Then, in the delegate method, here’s how I’d get the associated feed:

<code>feed = objc\_getAssociatedObject&#8203;(dataTask, associated\_feed);</code>

Of all the runtime things you can do, this has to be about the safest. It exists for situations like this one. It’s simple.

But still, it makes me feel a little weird.

#### userInfo

I’ll file a Radar. What I really want here is a `userInfo` property for <code>NSURLSessionTask</code>. It would take a dictionary and I could put whatever I wanted in there.

Even though using associated objects works, the APIs should handle reasonable and expected cases like this without making the developer have to choose a least-bad option.

#### NSURLSession Is Cool

Despite this one odd thing, I like the new `NSURLSession` a <em>ton</em>. I like the design, and I like that it makes some previously-difficult things easy. I like that we can do background tasks.

If you haven’t yet, you should read [From NSURLConnection to NSURLSession](http://www.objc.io/issue-5/from-nsurlconnection-to-nsurlsession.html) in the latest objc.io.

#### Update Oct. 17, 2013

A wise man clued me in to this: there are APIs for attaching data to an `NSMutableURLRequest`. I’d not noticed this part in `NSURLRequest.h`:

>`NSURLRequest` and `NSMutableURLRequest` are designed to be customized to support protocol-specific requests. Protocol implementors who need to extend the capabilities of `NSURLRequest` and `NSMutableURLRequest` are encouraged to provide categories on these classes as appropriate to support protocol-specific data. To store and retrieve data, category methods can use the <code>+propertyForKey:&#8203;inRequest:</code> and <code>+setProperty:&#8203;forKey:&#8203;inRequest:</code> class methods on `NSURLProtocol`. See the `NSHTTPURLRequest` on `NSURLRequest` and `NSMutableHTTPURLRequest` on `NSMutableURLRequest` for examples of such extensions.

Short version:

To attach data to an `NSMutableURLRequest`, write some code like this:

<code>[NSURLProtocol setProperty:someObject forKey:someKey inRequest:request]</code>

There are methods for getting and removing properties also.

So: problem solved. (Well. I haven’t actually tried it. But I have no reason to believe it wouldn’t work.)
