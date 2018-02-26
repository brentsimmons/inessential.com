@title Vesper Sync Diary #13: Unlucky Numbers
@pubDate 2014-04-13 21:35:00 -0700
@modDate 2014-04-13 21:39:11 -0700
I’ve been writing Cocoa apps for so long that I’m rarely surprised. I don’t know everything — surprises happen, and of course there are things that I know I don’t know — but, in the main, I know the intricacies well enough that I don’t even have to think about them.

But writing syncing means learning a new environment. For me it’s JavaScript, Node.js, and Azure. And I just ran across a big surprise in JavaScript.

If you have Node.js installed on your system, you can open Terminal and do this.

Launch Node. (Just type `node` and hit return.)

Copy-and-paste the following number and hit return: `9223372036854775807`.

Node evaluates the expression. What do you think you get?

<code>&gt; 9223372036854775807</code><br />
<code>9223372036854776000</code>

That’s right. It’s not the same number.

Some of you will note that the number I chose is the maximum value of a 64-bit integer. The problem occurs with sufficiently large integers. Here’s the deal: [JavaScript numbers are 64-bit floating point numbers](http://www.w3schools.com/js/js_obj_number.asp), which means they don’t have enough precision for very large integers.

I had no idea.

I should have known. Well, it’s a thing I needed to learn, and I just learned it.

#### Why Care?

When does a note-taking app need to deal with very large numbers? After all, if someone types a big number into a note, it doesn’t matter, because the entire note is treated as a string.

Here’s the thing: unique IDs for notes and users are 64-bit integers in my system.

So when the iOS app sends a note to the server, it sends a 64-bit integer along with note text and other properties of the note.

JavaScript code takes that data and then inserts the data in the database.

The “takes that data” part is where JavaScript turns the note’s unique ID from 9223372036854775807 (for instance) to 9223372036854776000 (for instance). We can’t have that.

#### Options

I’m writing this up as soon as I learned about it. I have to figure out what to do.

The first thing: user IDs might as well be 32-bit integers. (JavaScript can handle 32-bit integers accurately.)

Before we get anywhere near 2147483647 (max for 32-bit integers), we will have hired a team of the brightest server-side programmers in the world, and they’ll figure out what to do. 

But that still leaves note IDs.

#### Option 1: stringify

On the server side, treat the unique ID as a string. JavaScript won’t mess with it if it’s a string. Strings are tough and opaque.

Problem: database bloat. Storing strings takes up way more space than storing 64-bit integers.

Plus it’s inelegant.

#### Option 2: 32-bit integers

Collisions are more likely on assigning a random note ID when using 32-bit integers instead of 64-bit integers.

Now, the client app does check for collisions by looking at the note IDs it knows about.

But there may be a few note IDs it doesn’t know about (that haven’t been synced from another client, for instance).

That’s a very, very small risk. Most of the time there won’t be unknown note IDs, and when there are it will tend to be very few.

But still: ugh.

(Remember that global note ID collisions aren’t an issue. A given note ID has to be unique for a given user only.)

#### Option 3: 53-bit integers

The largest integer JavaScript can handle is 2-to-the-53rd power.

<code>&gt; Math.pow(2, 53)</code><br />
<code>9007199254740992</code>

The downside is still that there’s a chance of collisions — but, really, that’s a sufficiently large number size that I’m not at all concerned. (Remember that the client app checks, so the chance of a collision is really with a new note ID and any note IDs the client doesn’t know about yet, which will usually be zero anyway.)

And — it just occurred to me that I can add a second collision check: if a note comes from the server that matches the unique ID of an existing note, and the creation dates of the notes are not identical, then I can deal with that. (By giving one of the two notes a new ID and syncing.)

This is what I’ll do.
