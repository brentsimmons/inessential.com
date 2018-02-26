@title Vesper Sync Diary #6 - Merging Notes
@pubDate 2013-11-13 14:14:21 -0800
@modDate 2013-11-13 14:14:21 -0800
#### The Rules

1. Conflicts are not permitted.

2. A note should merge at the property level. (If you change note text on your day phone and a note’s tags on your night phone, both phones should get both changes.)

3. Real time determines which change wins.

4. A client doesn’t have to be up-to-date before it can push changes to the server.

5. The order of calls to the server must not matter.

6. It’s not important to keep a history of changes.

#### It’s not Like SCM

With SCM, changes have parents and children. SCM systems work wonderfully and we developers rely on them, but that model doesn’t fit here. I don’t care if change B descends from change A — the only thing that matters is that change B happened later in real time (wall-clock time).

This rules out <a href="http://www.cs.rutgers.edu/~pxk/417/notes/clocks/index.html">Lamport clocks</a>. They have their uses, definitely, but not in this case.

(I also rule out vector clocks, because the system would need to know about all the clients for a given user. Clients may come and go, which would make using vector clocks rather challenging. Even if I could use them, I’m not sure they’d enforce the real-time-wins rule.)

#### Last-Writer-Wins (to Server) Won’t Always Work

One simple way to make this work almost all the time is to say that the last change the server receives is the winner. (Many APIs work that way.)

The problem with that is when you make changes on your day phone, but it can’t connect to the server, then you go make changes on your night phone — then your day phone finally connects and overwrites the changes you made on your night phone. That violates rules #3 and #5.

Put another way: real time wins, but that has to be the real time that a person made a given change, not the real time that a change made it to the server.

#### How Merging Works

A note has a few properties that can change. (Text, tags, attachments, sortDate, archived status.)

For each of these properties there’s an additional property: a modification timestamp. (As in textModificationDate, tagsModificationDate, etc.) Those timestamps are set on the client: they’re the real time the user made that change.

Merging happens on both server and client, and it always happens the same way: when comparing a property, it compares the modification date for that property. The later modification date always wins.

This means that changes can arrive on the server and on clients in any order, delayed by any amount of time, and merging will always give the same result.

#### Why You Suddenly Feel Frightened

To the <a href="http://en.wikipedia.org/wiki/Fallacies_of_Distributed_Computing">Eight Fallacies of Distributed Computing</a> you could add a ninth fallacy: client clocks are accurate.

They’re not. You can’t rely on them. But if you can’t rely on client clocks being accurate, how can this system work?

I’ve had some advice on this.

One idea is to have the client check the time against a <a href="http://www.ntp.org/">Network Time Protocol</a> server (or the sync server, which is probably simpler). If the time is off by some substantial amount, then let the user know that syncing may not work correctly, and that they should turn on setting the time automatically on their device.

Another idea is to get the time from the sync server, compare it to the client time, and <a href="https://twitter.com/chockenberry/status/400684916670619649">calculate an offset</a> to use when creating timestamps. That should allow the client to create accurate-enough timestamps.

I like this second idea best. Given a server that reports its time with each call, clients get plenty of opportunities to recalibrate. (The offset calculation would have to take into account the duration of a given call. I’d probably just assume that the server date refers to a date duration-of-call / 2 seconds ago. Close enough.)

There would also be sanity checks. Is a calibrated timestamp way in the past or the future? Is a new calibrated timestamp earlier than the existing timestamp for a given property or earlier than the last date reported by the server? (It’s not allowed to be.) Easy stuff.

The worst-case scenario is a client where the time keeps changing wildly. But, with frequent recalibration and sanity checks, even this rare case should work fine.

#### Failure

Syncing is, like baseball, a game of failure. This system accounts for all of these failures:

1. Temporary network failure.

2. Temporary server failure.

3. Client clock failure.

4. Temporary failure to get a client up-to-date with sync changes.

5. Temporary failure for a client to send sync changes.

Once the failures clear up, everything will sync, and the result will be exactly the same as if there were no failures. (Note that client clock failure can be permanent and it will still work.)

#### How to Evaluate a Syncing System

I think a good syncing system has four attributes:

1. It does what the user expects.

2. It’s efficient.

3. It resists failures.

4. It continues to work.

I might add #5: it’s as simple as possible (though not simpler). Bugs are less likely when there’s nowhere they can hide. Achieving 1-4 is easier when the system is not complex.
 
What I like about this system is that it comes down to date comparison, and it’s hard to get simpler than that. Easy to write, easy to debug, easy to maintain.
