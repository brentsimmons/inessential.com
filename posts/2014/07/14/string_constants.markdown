@title String Constants
@pubDate 2014-07-14 11:56:16 -0700
@modDate 2014-07-14 11:56:16 -0700
Here’s my secret, or maybe my superpower, or maybe just me being lucky — I’ve never had a bug related to using a string literal when I should have used a constant.

But I *have* had bugs when I used the wrong string constant.

Here’s a line of code that just made the in-development app throw an exception:

<code>NSArray *uniqueIDs = [syncNotes valueForKeyPath:&#8203;VSSyncNoteIDKey];</code>

Looks good, right? But it’s wrong. I replaced it with this — and the bug was fixed:

<code>NSArray *uniqueIDs = [syncNotes valueForKeyPath:&#8203;@"uniqueID"];</code>

You’ve figured it out already, I’m sure — VSSyncNoteIDKey != @"uniqueID". VSSyncNoteIDKey is @"noteID", which is the server name for a note’s unique ID. The local storage name is uniqueID. And I picked the wrong one in that line of code.

The real way to fix it is this:

<code>NSArray *uniqueIDs = [syncNotes valueForKeyPath:&#8203;VSUniqueIDKey];</code>

(Which I changed it to after having to find the right constant for uniqueID.)

I know that using a string constant is the accepted best practice. And yet it still bugs me a little bit, since it’s an extra level of indirection when I’m writing and reading code. It’s harder to validate correctness when I have to look up each value — it’s easier when I can see with my eyes that the strings are correct.

I knew I wanted @"uniqueID" and could have typed that — yet I used VSSyncNoteIDKey (probably because that’s where autocomplete led me first, and it looked right).

I know the three knocks against using string literals:

* It’s hard to spot typos by eye.

* The compiler won’t catch errors.

* If you make a change, you have to change it in multiple places.

But I’m exceptional at spotting typos. And I almost never have cause to change the value of a key. (And if I did, it’s not like it’s difficult. Project search works.)

The question is: do I want to be the one guy who does what every other developer in the world thinks is terrible?

What if I believe, honestly and with good reason, that my using string literals would make for fewer bugs during development?

You’re horrified right now, I know, and you kind of wish I hadn’t posted this. (Think of the children!)
