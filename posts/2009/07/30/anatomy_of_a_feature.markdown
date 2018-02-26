@title Anatomy of a feature
@pubDate Thu Jul 30 09:38:01 -0700 2009
@modDate Thu Jul 30 09:38:01 -0700 2009
“Oh, it’s easy, just a quick http call. I could write a script to do it in like 20 seconds.”

I recently added a pretty easy feature to NetNewsWire — a Send to <a href="http://www.instapaper.com/">Instapaper</a> command. (It will appear in 3.2.)

It really <em>is</em> just a quick http call to the Instapaper server to <a href="http://blog.instapaper.com/post/73123968/read-later-api">add a URL</a> to the Read Later list.

Piece of cake.

But of course it’s not as simple as just writing a quick script. It’s tempting to think that adding a feature like this is just about adding the functionality — but there’s a bunch more to it than that.

### Decisions

It’s not enough just to write the basic functionality and add a menu item that runs it. Even a feature as simple as this one requires some up-front thinking, some design.

#### Should it support multiple Instapaper accounts?

This would complicate the feature. Each time you post you’d have to choose the account (if you have more than one).

And we’d have to include some UI for creating, adding, deleting, and editing your Instapaper accounts, which would require a whole new screen, probably in the Preferences window.

I’m willing to bet that most people who use Instapaper use just one account, or at least are willing to use just one account when saving from NetNewsWire. So I decided that support for multiple accounts was not nearly worth it.

But!

While a person may have just one account, they might change that one account some day. So I had to have a way to change your Instapaper credentials. I already knew I’d have a menu item — I took the simple way of adding an alternate item (that appears when you hold down the option key) for switching your Instapaper account, so you can enter new credentials.

I don’t necessarily love this, because it can be hard to discover — and sure as shootin’ I’ll get questions about it, even if it’s in the Help book — but at least the capability would be there for the rare times it’s needed.

#### Should there be a toolbar item?

Tough call. I decided no for 3.2, but yes for 4.0.

Toolbar items need artwork, and artwork doesn’t grow on trees: they cost money and time, and I’m on a tight schedule.

But still, this was a tough one, because I know there are users who barely look at menus. If a command is not in the window, they won’t know about it. To make things worse, even if I made the send-to-Instapaper command a default member of the toolbar, anybody who’d previously customized their toolbar wouldn’t see it. And they wouldn’t necessarily think to check if the toolbar has any new items with the new release.

Discovery is *always* an issue. And there are two types of feedback:

“I don’t know why you put that in my face — I’ll <em>never</em> use it.”

And...

“I don’t know why you buried that feature!”

#### Should it work like syncing?

If you’re offline or the Instapaper server is down (not that I’ve heard of it going down), and you choose Send to Instapaper, what should happen?

If it works like syncing, then it would try to contact the server, but if it fails, it would remember and keep trying later until it succeeds. Even across runs of the app.

If I did that, I’d have to:

- Add a persistent list (using a database, property list, Core Data, something) to remember URLs that need to be re-tried.

- Add code that keeps trying to send items from the list.

More importantly, I’d have to deal with the following user experience:

1. User does a send-to-Instapaper from within NetNewsWire.

2. The call fails for some reason and is queued up, to be re-tried later.

3. User goes to their Instapaper Read Later list and does *not* see the item they remember adding. User goes, “Whisky! Tango! Foxtrot!”; user is, quite rightly, less than happy.

There would have to be some kind of UI for dealing with this. It could be as easy as notifying the user that the call failed but would be re-tried — but, worse, I suspected that a way to view the queue would also be needed.

Which meant, probably, a new window with a table diplaying the queue, and another menu command to open the queue. And probably buttons for deleting items from the queue, and maybe a button to re-try all right away, and maybe some more info about the failures (the reason why the requests are queued). And there would probably have to be some indication in the main window that there are requests in the queue.

Totally not worth it.

The experience of most Instapaper users is with using a bookmarklet: they know that it won’t work if off-line, and they know that it tries once, right away. Given that, I could make it easy *and* do what current Instapaper users already expect: try the call, and if it fails, present an error message to the user.

#### How and when should credentials be entered?

The easy and obvious answer is to display a username and password sheet if you choose the command and haven’t entered credentials before. Because Instapaper has some special requirements, this couldn’t be a generic username/password sheet (one where I just update the text before displaying) — it needed its own sheet.

#### How should feedback be displayed?

This feature is different from the send-to-weblog, send-to-delicious, etc. features in that no more action is required after choosing the command. (Once you’ve entered credentials the first time, that is.)

Since NetNewsWire has a status bar, I decided that that’s the place for feedback: a spinning progress indicator and some “Sending to Instapaper...” text.

You’ll note that this got revisited later.

While thinking about all of the above, I actually wrote the simple little code that actually sends the URL to Instapaper. I barely remember doing it. It was a piece of cake.

#### What about sending multiple items at once?

My theory: anyone who needs to be able to send multiple items with one call is somebody who’s using Instapaper as storage rather than as a to-read-later list. I figured this wouldn’t be an issue for most people.

Consider the UI implications of partial success: say, for whatever reason, 3 out of 7 calls failed. How do you notify the user? It gets complicated and un-fun at this point.

So, no, just one item at a time.

### On to the implementation...

After all this, “Now vee may perhaps to begin.”

#### Menu items

I put the Send to Instapaper menu item in the News menu, next to similar items. Added the alternate Switch Instapaper Account... menu item. I gave the menu item a keyboard shortcut.

The next step was to validate the menu item: it should be enabled only when there’s a single selected news item or an open web page.

But, of course, that’s not enough — there is also the issue of contextual menus. There are several contextual menus where it was added:

- News items table.

- News item description.

- Tab.

- Web page open in tab.

#### The actual server call

This part was the easy part. Just a quick NSURL* thing. Cake.

#### Error handling

There is more error handling code than the code to actually call the server. It’s necessary to handle random connection difficulties, 403 authentication errors, bad-request errors, and so on. Any time an app makes an http call, all kinds of things can go wrong.

For example, if the server returns a 403, then it’s necessary to ask the user for credentials. Even if they’ve entered them before.

#### Authentication

There’s a special authentication sheet for posting to Instapaper. And a special window controller just for that sheet. Again, there’s more code there than for the http call itself.

Even just the code to get and set the password in the keychain is longer than the actual http-call code.

#### Feedback

When I first sent this to private beta testers, they liked the feature, but thought it should have some kind of feedback.

Well, of course there *was* feedback — some text and a spinning progress indicator in the status bar. But, unsurprisingly, people didn’t notice it.

I thought to myself, “You know, 10 years ago, that would have been fine. It would have been the right thing to do, to use the status bar.”

And I wondered why that was no longer true. The answer, I think, is monitor size. With bigger displays people create bigger windows, and it’s much less likely they’ll notice something in the status bar, since the status bar is so much farther away from where their focus is.

I went back to the drawing board and did a little popup window. My first quick version just had the Instapaper icon and a spinning progress indicator. I figured I’d add some “Adding to Instapaper...” text of some kind to it.

The code behind the feedback window is, again, bigger than the http-call code. (By now you’ve gotten the idea that the core functionality of a feature is often the very smallest part.)

When I first saw the feedback window in action, it happened so quickly that I realized it doesn’t need a “Posting to Instapaper...” message on it. In fact, that would have been a <em>bad</em> idea, since it happens so quickly you don’t even have time to read any words. So I left it at just an icon and a spinning progress indicator.

A reasonable question you might ask: why not just use Growl?

Two reasons.

- Not everyone has Growl.

- You want feedback to appear immediately — you want to know that <em>something is happening</em> right away, and you want to see that it’s continuing to happen. You don’t want to wait for a Growl notification.

And it’s nice that the feedback is similar to how the send-to-Instapaper bookmarklet works, so it will feel familiar to Instapaper users.

#### Finally

Private testers eventually got the new version with the feedback window, and I don’t have any bug reports. But of course I do have feature requests to implement all the things I decided not to do or to leave for later. Plus more things — an entire Instapaper treatment, even, with the ability to see your reading lists in NetNewsWire and create groups and so on.

Applying the 80/20 rule means you <em>will get feature requests from the 20</em>. (And beta testers are often power users, and they’re more likely to want those extra powerful features.)

But, in the end, this was an easy and small feature.
