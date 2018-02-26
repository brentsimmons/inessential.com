@title Swift Diary #9: Where I’m Stuck
@pubDate 2015-08-05 10:24:55 -0700
@modDate 2015-08-05 11:41:25 -0700
Let’s say I’m writing a multi-platform social networking client. I know a person, and I have it on strong authority that Jack Dorsey’s going to re-open the Twitter APIs. (I can say this out loud because it sounds like I’m just pretending.) So my social networking client will support Twitter, App.net, LinkedIn, and a handful of other systems. (Let’s say.)

I’ve got the problem that <a href="http://inessential.com/2015/07/19/secret_projects_diary_2_swift_2_0_prot">I’ve written about before</a> — protocols and collections don’t mix well.

I’m using a protocol for the Account type. There are classes that conform to the Account protocol: TwitterAccount, AppNetAccount, LinkedInAccount, etc.

There’s also an AccountManager class that manages the accounts list. The list is a <code>Set&lt;Account></code>, as it should be (since no account should appear more than once; since ordering isn’t important).

Except, of course, no it isn’t, because Account is not Hashable.

In reality it’s an array — <code>[Account]</code> — that holds all the accounts. That’s fine. That works.

Except when it doesn’t: except when I want to see if the array contains an account object. Error: <code>cannot invoke 'contains' with an argument list of type '(Account)'</code>

So I can’t do manually what a Set would do automatically, which is to ensure that a given account appears only once.

And, here’s the thing: this scenario doesn’t appear once but a bunch of times. (A major example is the TimelineItem protocol. Each different type of account has one or more different TimelineItem-conforming classes, and a given timeline can contain multiple different concrete TimelineItem objects.)

I’ve worked around some of these, and I’m sure I can come up with work-arounds for each case. But it’s getting increasingly frustrating. It’s slowing me down.

I have some options:

* Continue with the work-arounds, despite the frustration. (Even though these projects are supposed to be *fun*.)

* Switch to Swift plus Objective-C types — that is, make Account and TimelineObject @objc protocols and make the classes that conform to those protocols @objc types. Then use Foundation collection types NSSet and NSArray. (This is like writing Objective-C with Swift syntax.)

* Switch to Objective-C, which handles my design perfectly. But is not Swift.

I don’t know what to do. What would you do?

<p style="text-align:center">* * *</p>

<b>Update 10:40 am</b>: Some people are asking why Account can’t be Hashable. It’s because it can’t be Equatable. (For starters. There might be other reasons too.)

<code>protocol Account: Equatable {</code><br />
<code>&nbsp;&nbsp;var accountID: String {get}</code><br />
<code>}</code><br />
<code>func ==(lhs: Account, rhs: Account) -> Bool {</code><br />
<code>&nbsp;&nbsp;return lhs.accountID == rhs.accountID</code><br />
<code>}</code>

Error: <code>protocol 'Account' can only be used as a generic constraint because it has Self or associated type requirements</code>.

If there’s an answer to this, then I’d be extremely keen to know what it is!

<p style="text-align:center">* * *</p>

<b>Update 11:00 am</b>: Got Equatable working, <a href="https://twitter.com/optshiftk/status/628985834801336320">thanks to Kyle Sluder</a>, but not Hashable. <a href="https://gist.github.com/brentsimmons/beba6ec62302dfe09070">Here’s my current gist</a>.

<p style="text-align:center">* * *</p>

<b>Update 11:10 am</b>: I spoke too quickly. Equatable is still the problem. <a href="https://gist.github.com/brentsimmons/7ec7e3669ff7ad17e446">Here’s the gist</a>.

Which means I’m faced with the original point of this post. What to do?

<p style="text-align:center">* * *</p>

<b>Update: 11:35 am</b>: Several people have suggested using a base class instead of a protocol. That should do the trick, yes.

But there were reasons to use protocols in the first place:

* I dislike class inheritance in general.

* I don’t like using a base class purely to satisfy the type system.

* Requiring a base class makes doing a plug-in API more difficult. (It’s simpler to have plug-ins conform to a protocol. Though I have to admit I haven’t done any research with Swift plug-ins, so it’s possible I’m completely optimistic here anyway.)

I’m pragmatic, though, and I may end up doing this as a work-around.
