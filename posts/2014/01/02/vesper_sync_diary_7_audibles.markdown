@title Vesper Sync Diary #7 - Audibles
@pubDate 2014-01-02 13:49:27 -0800
@modDate 2014-01-02 13:49:27 -0800
I described the plan in earlier sync diaries. And then I started writing code.

You know how it goes: things look one way when you’re in the huddle, and quite another way at the line of scrimmage.

#### Attachment Metadata

(Attachment metadata is unique ID, size in bytes, MIME type, and height and width.)

To recap: the sync code supports multiple attachments per note, whether we ever use that feature or not.

So, unsurprisingly, I decided that there should be a database table for attachment metadata (on both client and server), and each note would have a to-many relationship to its attachments. (The inverse relationship is to-one: an attachment belongs to a single note).

That’s how you’d do it; that’s the *right* way to do it.

But there’s a cost to this approach. Either:

*Notes and attachment metadata are synced separately*, which means that a client could have an incomplete object graph (it might have a note minus its attachment metadata).

Or…

*Notes and attachment metadata are synced at the same time*, but the server code is more complex and includes more database hits than I would like.

Incomplete object graphs are a major pain to deal with and they make for a bad user experience. So I ruled out the first option.

I didn’t like the second option either, for two reasons:

1. It’s very important to make the sync code as simple as possible, so that bugs have nowhere to hide. (Syncing is difficult, so I’ve adopted an extreme committment to simplicity.)

2. It’s very important to make syncing as fast and efficient as possible, so that the app provides the best possible user experience.

So I decided to do what is arguably the wrong thing, but is the right thing in this context.

#### What I Did

Database people are already gasping for air, because they know what’s coming. Instead of creating a separate table for attachment metadata, I created an attachments column in the notes table and just encoded the attachment metadata there.

On iOS it uses Core Data’s built-in object archiving feature. On the server it’s stored as JSON.

This is wrong, surely; it’s not how to do this. Except, in this case, it is. Incomplete object graphs are wrong; inefficient and slower syncing with more complex server-side code is also wrong.

This is *less wrong than the alternatives*.

With this change, a note always has its attachment metadata. Fetching notes always includes that data, on both client and server. They’re inseparable. And it means just one database hit to fetch a set of notes.

Some of you are gasping for air anyway. I know.

#### What I Gave Up

With this configuration it’s more difficult to do a query against attachment metadata. Not impossible, but more difficult, and it would probably involve some filtering in code. That’s not great.

But the app doesn’t make any queries like that, and we don’t have any features on the horizon that need that.

Still, I could have insisted on planning for that contingency. After all, I’m already planning for the possibility of multiple attachments per note. What makes one contingency different from another?

I look at it this way: supporting multiple attachments is a more obvious feature than some unknown feature that requires queries against attachment metadata. I don’t even know what that feature would *be*. And if it hasn’t come up in the first six months, there’s an excellent chance it would never come up.

Or, put another way: is planning for that remote contingency worth degrading user experience? Is my notion of database-correctness more important than simpler code and fast and efficient syncing?

Nope.

But what if it *does* come up some day? Well, it’s just software, and I’ll make it work by doing the smartest things I can think of. Like always.
