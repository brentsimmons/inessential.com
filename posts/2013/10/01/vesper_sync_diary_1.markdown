@title Vesper Sync Diary #1 - Syncing Tags
@pubDate Tue Oct 01 12:26:24 -0700 2013
@modDate Thu Oct 03 16:50:19 -0700 2013
Because we [announced that we’re working on syncing](http://daringfireball.net/2013/09/vesper_whats_new_whats_next), I have the luxury and fun of being able to narrate my work.

I’m thinking about syncing tags.

My first thought is to assign each tag a unique ID (a UUID). This has the advantage that if a tag is renamed (not promising that feature), then it’s easy to sync that name change. Tags might look like this in the database:

<code>name: Cars<br />
uniqueID: 436BF0FC-E264-45EC-&#8203;ACD9-C1A363845FC7</code>

<code>name: Radios<br />
uniqueID: A758512C-7B20-4F5F-9C4B-B40BE0BC2220</code>

And then a note would refer to its tags via an array of uniqueIDs. Something like this…

<code>tags: 436BF0FC-E264-45EC-&#8203;ACD9-C1A363845FC7, A758512C-7B20-4F5F-&#8203;9C4B-B40BE0BC2220</code>

…would translate to `Cars, Radios`.

So you could rename `Radios` to `Car Radios` with just a simple change. That tag would change in the database to look like this:

<code>name: Car Radios<br />
uniqueID: A758512C-7B20-4F5F-&#8203;9C4B-B40BE0BC2220</code>

And the note wouldn’t have to change, since the unique IDs of its tags haven’t changed. All that’s changed is the `name` field. Nice.

#### But here’s the problem

You have a day phone and a night phone. (Imagine.)

You’re thinking about your upcoming trip to Paris. On your day phone you create a `Paris` tag. But your day phone is off-line, and you switch to your night phone before your day phone gets the chance to sync.

So now it’s night-time, and you’re still thinking about your upcoming trip to Paris. On your night phone you create a `Paris` tag too.

Now you’ve got this situation with tags:

<code><b>Day phone</b><br />
name: Paris<br />
uniqueID: 92B6E1D4-C49A-4D74-&#8203;A0C3-C120B67EE5E9<br />
<b>Night phone</b><br />
name: Paris<br />
uniqueID: B0F4EFD6-9953-4CFD-&#8203;ADBB-FE1CFAFD22D3</code>

That’s really two separate tags, since they’re referenced by uniqueID instead of name. Notes on your day phone refer to 92B6E1D4-C49A-4D74-&#8203;A0C3-C120B67EE5E9; notes on your night phone refer to B0F4EFD6-9953-&#8203;4CFD-ADBB-FE1CFAFD22D3.

I don’t like that. You don’t like that.

#### How I think I will solve the problem

Instead I’ll give each tag a uniqueID that changes when the name changes. The uniqueID will be the name transformed to lower-case. (So that `Paris` and `paris` have the same uniqueID.)

This solves the day/night phone problem like this:

<code><b>Day phone</b><br />
name: Paris<br />
uniqueID: paris<br />
<b>Night phone</b><br />
name: Paris<br />
uniqueID: paris</code>

Same! Cool.

This makes renaming tags more difficult, though. In this scenario, a note’s list of tags looks like this:

<code>tags: cars, radios</code>

So when you rename `Radios` to `Car Radios`, it’s necessary to update every single note that references `radios` so that it looks like this:

<code>tags: cars, car radios</code>

That’s more work when renaming, but I think the trade-off is worth it so that your day and night phones don’t clash when you create the same tag on each device before they sync.

#### But what about deleting tags?

(Not promising this feature either, but I have to code for it.)

After your trip to Paris you delete the `Paris` tag. One way to handle this is to make the tag entry look like this:

<code>name: Paris<br />
uniqueID: paris<br />
deleted: YES</code>

Just flip the `deleted` bit to YES, and that’s the entire change. The app would be smart enough to know that if a note refers to the `Paris` tag, it should just ignore it, not show it, since that tag has been deleted.

One small change and you’re done. Nice.

But no…

Six months later you have another trip to Paris. So you’re writing a note and give it a `Paris` tag. What should happen then?

Well, we could flip `deleted` back to NO. But then all the notes from your previous trip would all of a sudden have their `Paris` tag resurrected.

You don’t want that, because you’d deleted the `Paris` tag back then. You just want *new* notes tagged with `Paris` to show that tag.

#### How I think I will solve the deleting problem

The right thing to do is, once again, more work. The app will visit all the notes that refer to that tag, and remove that reference.

If a note has tags like this…

<code>tags: paris, packing, travel</code>

…then it would be changed to look like this:

<code>tags: packing, travel</code>

The actual tag could remain in the database — it’s just that no notes would refer to it. In the case of tags, that’s the equivalent of deleting it.

And if you started using that tag again in the future, it would, correctly, appear just for new notes. It wouldn’t get resurrected for old notes, since those notes were changed to not refer to that tag.

#### Note

I’m still thinking about tags. I could change my mind (particularly if I think of a better way, or if someone tells me about a better way).

Much of the rest of syncing is conceptually nailed down. (Much of it was nailed down before I wrote the first line of Vesper code last February.) But things can change as theory meets code.
