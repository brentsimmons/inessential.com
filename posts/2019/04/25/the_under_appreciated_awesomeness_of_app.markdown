@title The Under-Appreciated Awesomeness of Apple Events (the Technology)
@pubDate 2019-04-25 16:41:59 -0700
@modDate 2019-04-26 14:31:50 -0700
Picture Jane in her office. She gets an email from Bob every month with the latest WidgetX numbers. With that email in front of her, she double-clicks a script (or chooses one from a scripts menu), which:

1. Grabs the text of that email
2. Extracts the actual numbers (minus Bob’s signature, etc.)
3. Tells FileMaker Pro to open a specific database, and then adds those numbers to the database
4. Creates an HTML page from a template, including the new numbers
5. Uploads that HTML page to the company’s internal CMS
6. Creates and sends an email (via Mail), with the new numbers, that goes to the CEO
7. Updates and saves (on a shared folder) a Keynote presentation with the new numbers

This used to take hours, and it was prone to errors. Now it takes a minute or less — and it’s error-free.

What’s going on here? It’s AppleScript, sure — but, under the hood, it’s Apple events.

### How to save a computer company

Apple events (lowercase “e” is correct) arguably saved Apple in the ’90s. Desktop publishing was huge and very Mac-centric, and that was in part because the various tools were *automatable*. When you can automate, you can save time and money.

This was before Mac OS X: there was no UNIX automation. No shell scripts, no pipes, no Terminal.

Instead, there was AppleScript and UserLand Frontier and an underlying bit of technology called Apple events. And apps like QuarkXPress which were scriptable.

You might say that Steve Jobs — or the iMac or the iPod or NeXT technology — saved Apple. But it’s very possible that Apple, without automation, might not have lasted long enough to get to Steve Jobs.

### What Apple events are

Roughly put — they’re a way of calling a function, with parameters, in an app and getting back a result.

There are a few key things to know:

* The other app is an already-running instance: Apple events do not result in a new instance of an app (exception: if an app isn’t running, you can, conveniently, launch it via an Apple event)
* The function parameters are not limited to strings — you can send binary data (image data, for instance), arrays, etc. (This is key: the API is much richer than just a URL scheme with some text, which is what we’re limited to on iOS)
* Apple events are an underpinning of AppleScript, but they’re not limited to AppleScript — they can be sent and received programatically by any app

Mac developers will often use Apple events without even realizing it. For instance, there are methods in `NSWorkspace` that hide underlying Apple events: opening a URL in the browser, or opening a Finder window rooted at a given folder.

These work because the browser and the Finder respond to specific Apple events, and NSWorkspace knows how to send them.

Another key thing to know: this was early ’90s technology. It survived the transition to Mac OS X because people relied on automation — particularly, as I mentioned, for desktop publishing, but for other purposes too — and, without that automation, they would have left the Mac.

When I say “relied on,” I mean that there were companies whose profits relied, at least in part, on being able to automate away hundreds of hours of manual tasks.

And there are plenty of people today who rely on Apple events to get their work done. It’s quite common.

### Apple events are an example of the genius of the Mac

The Mac, the “computer for the rest of us” — for those of us who didn’t want to deal with a DOS prompt and arcane stuff — always promised to be easy for novice users. The UI was consistent, which helped a ton. Designers were encouraged to make commonly-used features the most visible and easiest to use.

And that’s great — but the absolute genius was combining that with power-user features by way of *progressive disclosure*.

This meant that more power was there, but it wasn’t required in order to use the app well. But, once you needed it, you could find it. And that extra power was as well-designed as the rest of the app, so you could get the most bang for your click.

But what do you do about features that shouldn’t actually be baked into the app? What about the power to do what Jane does?

That’s where automation — Apple events — comes in. It doesn’t get in the way of the UI, but if you can find your way to Script Editor (or a similar app: there are others), you can learn how to write any feature or workflow you can dream of (as long as it’s technically possible).

Part of the genius of this is that you’re scripting the apps you already use. You’re scripting these great GUI apps that you know and love. No command line, no piping/launching/closing. Just pulling information from apps and telling them to do things.

### The Mac OS X Accelerator Pedal

I have heard — I don’t know if it’s true — that some people at Apple wanted to ditch Apple events (and AppleScript) in the transition to Mac OS X. It was already a several-year-old technology, and I can see how people thought it might not fit in with OS X.

But the technology was preserved, as I mentioned earlier, because people and companies *needed it*. So it’s old stuff, but it’s stuck around for very good reasons.

But here’s where the Mac gets *even better*: OS X is UNIX, and now we can mix-and-match traditional Mac scripting with Python and Ruby and shell scripts and all the power of UNIX tools. (Note: you can call an AppleScript script from a shell script, and vice versa.)

I didn’t mention it, but Jane, in the example at the top, is using [AWK](https://en.wikipedia.org/wiki/AWK) to extract the numbers from Bob’s email text.

An outside observer might think Mac users just use pretty — and pretty simple — apps, and that’s the whole story. But that completely misses the power and genius of Macs.

I can’t think of another platform with the sheer level of automation power that OS X (now macOS) has.

### So, after all that, a question

What happens to Jane if Mail is a Marzipan app that doesn’t respond to Apple events?
