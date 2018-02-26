@title How Not to Crash #7: Dealing with Nothing
@pubDate 2015-05-29 10:35:46 -0700
@modDate 2015-05-29 10:35:46 -0700
Consider this line of code:

<code>[thing doStuff];</code>

If `thing` is nil, it’s no problem. No crash. Nothing at all happens.

But you can’t generalize from that that nil is okay in all cases:

<code>[self doStuff:thing];</code>

If `thing` is nil, then what happens? If depends on the implementation of `doStuff:` — it might crash. Consider this code:

<code>menuItem.title = thing;</code>

If `menuItem` is an NSMenuItem, then it crashes when `thing` is nil. The header for NSMenuItem doesn’t say that, and the documentation only hints at it (“If you do not want a title, use an empty string (@""), not nil.”)

This means you need to make sure `thing` is non-nil. You may be quite certain that it’s non-nil. But consider a case I once fixed, where `thing` was the name of a font. There was no reason for me to expect that the system API for getting a font name would ever return nil — except that it did, sometimes (rarely, of course, and never on my machine, no matter what I did).

Things to know:

Nil receivers are okay — as long as your code is okay with nothing happening.

Nil parameters may or may not be okay. When calling system APIs, the headers and documentation don’t always tell you what could happen. (This may change when they make greater use of [nullability annotations](https://developer.apple.com/swift/blog/?id=25).)

Trust no one.

#### Assertions

Assertions are a great way of documenting assumptions and requirements, and of making sure those assumptions are true. Assertions should not run in the release build (see the ENABLE\_NS\_ASSERTIONS Xcode setting).

One of my favorites is NSParameterAssert, which I use almost exclusively as a nil check for parameters that must not be nil.

It’s super-easy to use:

<code>- (void)someMethod:(id)someParameter {</code><br />
<code>&nbsp;&nbsp;NSParameterAssert(someParameter);</code><br />
<code>&nbsp;&nbsp;…do whatever…</code><br />
<code>}</code>

In the future I’ll probably start using nullability annotations *and* NSParameterAssert. Both. (I’ll also write some Swift code in the future, which is a whole other thing when it comes to nil. But I’m not talking about that today, partly because I’m not yet enough of an expert in Swift to have good advice.)

I also use NSAssert fairly often. NSAssert takes an expression, and a comment — but I’m lazy, and I make the comment nil. (Which is fine in this case.)

<code>NSAssert(something == somethingElse, nil);</code>

(A note about laziness: the lazy programmer doesn’t write crash bugs, because they don’t want to fix them later.)

#### My favorite crashing bug

Years ago, my app NetNewsWire had a crash-log catcher. At launch it would grab the latest crash log from disk and offer to send it to me.

With some OS X release (10.5, I think) Apple changed the format for crash logs on disk. I think they had been one file per app, and Apple switched to one file per crash. I had to write new code to handle the new format.

I made the change. It went to beta testers, who used the app extensively. Weeks passed. All good.

Then, on the day I released this version, I got a ton of reports from people who said, “It’s crashing on launch! But it works fine after launching it again.”

Here's the deal: the new code crashed when there were no crash logs at all. And then, on the next launch — now that there’s a crash log — it would not crash. (Yes, a *self-healing crashing bug*. In the crash log catcher. Such meta.)

Of course this meant that it crashed immediately for all *new* users, not just for people who’d been lucky enough never to get a crash.

This was a big reminder to me: *always consider the case where there’s nothing*. Nothing happens all the time. Nothing is pretty normal. But it might take special handling, and it should always be considered.

#### A less cool crashing bug

I don’t think this shipped — I think it was just in beta code.

Vesper syncing talks to a server. The server returns JSON data. The Cocoa JSON deserializer turns JSON nulls into `NSNull` objects.

Vesper was expecting an NSString, and got an NSNull. Vesper tried to call a string method on that NSNull, and it crashed.

On the surface this seems like a tough case, because you can’t be sure that the type of a given object in JSON text will be what you expect. You’re looking for a string and you get an NSNull.

Well, NSNull is one of those things you want to keep as isolated as possible. It’s a walking code smell (though I don’t know what an alternative would be in the case of JSON nulls). (And you should never deliberately use it outside of JSON. Almost never. Super-duper-rare. Like once every few years, and only if you really, really have to. Maybe not even then.)

This is part of why, as I [mentioned previously](http://inessential.com/2015/05/22/how_not_to_crash_4_threading), I like to turn JSON into intermediate objects. A big part of this is centralizing the handling of NSNull objects — I don’t want them to leak out into other parts of the app, where anything they touch turns stinky.

But there’s another point, which is this: *whoever wrote the server side is your sworn enemy*. He or she hates you very, very much.

Now, in the case of Vesper, that was me. But I still have to code as if the server author has my personal and professional destruction as their sole motivation. (Even though I know the guy, and he’s cool. He likes kittens.) And that doesn’t mean just checking for NSNull — which is normal in JSON anyway — but being careful with the types of every single piece of data.

Anything could be anything, at any time.

(It’s not turtles all the way down. You’re expecting turtles — but that would be too easy. It might be nothing all the way down.)

#### Total other thing

Initialize your variables. Just do it. If I had a nickel for every crashing bug I’ve fixed just by initializing a variable to nil — well, I’d have some nickels. You want zero nickels.

Not initializing your variables is like playing with gasoline and saying it’s okay because the matches are in your pocket.
