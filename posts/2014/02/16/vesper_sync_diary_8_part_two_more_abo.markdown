@title Vesper Sync Diary #8 part two - More about Unique IDs
@pubDate 2014-02-16 12:43:36 -0800
@modDate 2014-02-16 13:05:15 -0800
I’ve done some more thinking about <a href="http://inessential.com/2014/02/15/vesper_sync_diary_8_the_problem_of_un">the problem of unique IDs</a> and <a href="https://twitter.com/brentsimmons/status/434936886839087104">discussed it a bunch on Twitter</a>.

Some new thoughts:

#### Why I can’t use creation date as client ID

It doesn’t matter that the date might be inaccurate — the important thing is that it would be unique for a given person.

But I forgot to consider automation (scripting, importing) which could generate non-unique creation dates.

So using creation date is out.

#### Looking again at client-created IDs

I’ll recap this idea.

The client generates an ID. That ID needs to be unique for a given account. I’d use a UUID, which is an 128-bit number. (That’s double the ideal size of an ID, but I’m not too concerned about that.)

(A UUID is necessary because there’s no way to coordinate an incrementing 64-bit number.)

This solves the case where a user signs out of their account and signs in with a different account (which may or may not be new). Those client-generated IDs would survive this process — which is what I want. Though notes under a different account are different notes, and would get stored as such on the server, those same client IDs would be fine since the server enforces uniqueness on account ID + client ID.

What worried me last night, though, was the bad client scenario. An attacker.

#### A digression about security

I design as if anything can happen. An example: what if the server-side code got leaked? Would the system be hackable? (No.)

What if the client-side code also got leaked? (Still not hackable.)

But let me be more specific: if an attacker knows the API *and* has a user’s credentials, that attacker could conceivably access and change that user’s data.

I don’t know of a way around this.

But this is no different from any other service. For example, if you learn my Twitter credentials, you can tweet as me. (You don’t even have to reverse-engineer the Twitter API first.)

#### Bad clients and client IDs

The scenario that worried me last night was the attacker who figured out our API and had a user’s credentials.

That attacker could supply bogus client IDs for notes.

The damage would be limited to just that user, since uniqueness is account ID + client ID. (That attacker wouldn’t get access to data from another user, in other words.)

Also: if the attacker supplied bogus client IDs that were actually unique for that account, it wouldn’t matter. The system would work properly.

Furthermore, I could add a check: two ostensibly-the-same notes identified by client ID + account ID must have the same creation date, since creation date can’t change. Otherwise it’s an error.

But here’s why this scenario isn’t worth worrying about: what are the chances that an attacker just wants to screw around a little by supplying bogus IDs?

Most likely that attacker would do much worse things. (Consider that someone hacking my Twitter account wouldn’t want to do some slight and hard-to-detect mischief — they’d do something more dramatic.)

The only scenario that I can think of where an attacker supplies bogus IDs is where they’re trying to get information from other accounts. But we’ve made that impossible by saying that IDs are unique only to a given account. (Lookups on the server are *always* done with an ID/accountID pair.)

#### Going with client-generated IDs

That’s the upshot. I’m going with client-generated IDs.

<i>Update 1 pm:</i> Regarding coordinating incrementing a 64-bit integer, <a href="https://twitter.com/optshiftk/status/435156076711796736">Kyle Sluder reminded me of vector clocks</a>. Good point, but not worth the trouble here.
