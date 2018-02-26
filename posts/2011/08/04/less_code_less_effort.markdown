@title Less code, less effort
@categoryArray Cocoa-Development
@pubDate Thu Aug 04 13:55:26 -0700 2011
@modDate Thu Aug 04 14:20:50 -0700 2011
Here are a few things I’ve been doing lately to write better code, and less code, with less effort.

#### Synthesized instance variables

Adding a property is costly when you have to declare it three times: once as an instance variable, once (or twice) as a property, and once with @synthesize.

Last year I had tried synthesized instance variables, where you only have to declare it as a property and with @synthesized. I remember being disappointed because the synthesized variables didn’t show up in Xcode’s debugger.

Then I tried it again the other day, and the variables appeared. Somehow I’d missed the memo that it works now.

I promptly went through and deleted all the instance variables from my app. They’re now all synthesized.

#### Automatic Reference Counting (ARC)

For anyone who’s been writing Cocoa apps for a while, manual memory management is second nature. Me, I don’t even think about it. Errors are extremely rare (but they can happen).

I took a few hours the other day and converted my app over to ARC. That meant deleting a whole bunch of code: no more retains, releases, and autoreleases.

I also deleted a whole bunch of dealloc methods. (When I had to keep a dealloc method, it was just to remove the object as an observer.) If you think about it, dealloc was, in a way, yet a fourth place where you had to declare a property. (Once as ivar, once or twice as property, once using @synthesized, and once in dealloc. Crazy. That’s the kind of thing that makes programming a chore.)

Less work, less chance of error. ARC’s cool.

#### valueForKey on arrays

If you write code that works with a database or via web services, there’s a good chance you’re dealing with unique IDs of some kind, and there’s a good chance you need to get an array of those IDs sometimes.

The way I used to do this:

<pre>NSMutableArray *arrayOfIDs = [NSMutableArray array];
for (RSFoo *oneFoo in someArray)
   [arrayOfIDs addObject:oneFoo.uniqueID];</pre>

There’s an easier way:

<code>NSArray *arrayOfIDs = [someArray valueForKey:@"uniqueID"];</code>

This isn’t particularly new, but I used to always forget about it. (Obviously, it’s useful not just for unique IDs. I just mentioned that because it’s a common case for me.)

#### Configuring rather than coding

My app makes 25 or so different calls to our platform. I wrote this as one base class and 25-ish subclasses.

That’s not wrong, but it <em>totally and completely sucks</em>. It means 50 files to manage. It means creating two new files and coming up with a new class name every time I want to add a new call — and it means a new chance for errors and bugs.

What I noticed about these subclasses is that they only two do things:

1. Configure the call before sending it. (Set the HTTP method, set the URL, add parameters to the right places.)

2. Turn the result into an object. (Usually that means taking the result of the JSON parser and turning it into a model object.)

I’m in the middle of getting rid of all these subclasses. Instead, each API call is defined by a struct, and those structs all live in a single file.

<pre>const RSAPICallSpecifier kGBAPICallDownloadNotifications = {
   .httpMethod = kHTTPMethodGet,
   .path = "notifications/",
   .returnType = RSHTTPReturnTypeJSON,
   .returnedObjectClassName = kGBNotificationParserClassName,</pre>
etc...

I could have used a plist or something else. The point is that how-the-API-works is a form of data, and I can separate that from the code that talks to the server. That makes it easier to make changes and additions. It means less code to read and write and manage, and fewer chances of errors.

(For bonus points, our API description would be on the web in some parseable form, and I’ve have a script that downloads that data and then rebuilds those structs, and also alerts me to what’s changed. Not a new idea, no.)

#### Blocks and GCD

I don’t mind the formality of delegates and protocols — except that it does mean more typing. There are plenty of times when creating an API that takes a block will save a whole bunch of work and be just as clear, if not more clear. So I do.

I’m a big fan of NSOperationQueue, but it usually means creating a class, overriding the right methods, and so on. There are times when GCD will do instead. So I use that also.

Here’s how I split it up: I use NSOperationQueue when I have something somewhat long-running. I want to set priorities and dependencies, and I want to be able to monitor and potentially cancel operations. The main use is for downloading things: making calls to our server, downloading thumbnails and images, that kind of thing.

But I’ve slowly come around to seeing that there are cases where GCD is perfect for me. An example is rendering images — for instance, if I want to create an image with rounded corners and a drop shadow, I do it in the background via GCD. There’s no need to monitor these or be able to cancel them.

#### NSCache

It may be my best friend. I toss in rendered images, text measurement calculations, strings that are expensive to calculate, etc.

I used to have all kinds of different caches, and now I use NSCache almost exclusively. (There are rare cases where I might use an NSMutableDictionary or NSMutableSet.)

It’s super-easy to use — like an NSMutableDictionary, it responds to <code>objectForKey:</code> and <code>setObject:forKey:</code>.

Particularly cool is that an NSCache handles removing items itself. I don’t have to think about it. It means fewer things I need to do when getting a memory-warning message.

#### Xcode 4 text snippets

I was bummed at first to lose the Xcode scripts menu. (My hope is that I can replace the features I miss via AppleScript and <a href="http://www.red-sweater.com/fastscripts/">FastScripts</a>.)

But having the text snippets is *way* better than the previous system for adding completions. Drag some text in, give it scope, title, and completion shortcut, and you’re good. It works, and it’s worth doing.

(There are a few things I wish for, though. User-entered snippets should be at the top, not the bottom, since they’re probably more important. And it’s silly that to remind myself of a completion shortcut I have to double-click the item and then click Edit. It should just be part of the display in the table. [I’m a developer. <em>Please</em> don’t make me click so much.])

#### Some things I still wish for

I wish I didn’t have to use @synthesized. I’d love to be able to declare a property exactly once.

I wish Xcode’s autocomplete would still work before I’ve imported the header file for a class that it totally knows about. It means I have to stop my typing, go to the top of the file, import the right .h file, then try to find my way back to where I was. (The back command should work after a cmd-upArrow.)

I wish Xcode would just add import statements for me when it’s unambiguous. (I’d wish away header files and imports entirely if I could.)

I wish I didn’t have to delete the DerivedData folder when things go wrong. I wish I didn’t have to delete xcuserdata when Xcode stops being able to keep up with my typing (on an 8-core Mac Pro).

I wish I could type <code>someArray[0]</code> and have it mean <code>[someArray objectAtIndex:0]</code>. Similarly, I wish I could type <code>someDictionary['someKey'] = someValue</code>.

I wish dot notation worked all the way through, as in <code>someView.frame.size.height = whatever</code>.

I could go on and on. Which is just to say that things are getting better — we’re able to do more with less work — but there’s always room for improvement. Gives me something to look forward to.
