@title Setting Expectations About CloudKit
@pubDate 2014-07-28 09:06:56 -0700
@modDate 2014-07-28 10:06:58 -0700
Macworld: <a href="http://www.macworld.com/article/2455127/why-you-should-care-about-cloudkit.html">Why you should care about CloudKit</a>:

>The big difference is that the information stored in it can be made available to multiple users, allowing them to collaborate and share information through the cloud—something that iCloud “Classic” was unable to do…

>Don't let the term “public” put you off, though—CloudKit doesn't force all the shared data in a big bucket that is automatically visible to everyone who installs a particular app. Instead, developers will be able to protect the information as they see fit, allowing, for example, users from a particular group or organization only to have access to specific content…

>It’s not hard to see that CloudKit greatly simplifies the creation of apps that revolve around multi-user collaboration. Previously, creating a group chat app like Glassboard, or a team-based task management software like Wunderlist, would have required a significant amount of work.

I don’t see how this is true. While it’s technically possible to use the public data for group collaboration, it’s only the code in the client app that enforces this. CloudKit has no notion of groups.

It would be irresponsible to use the public data for private group collaboration.

Neither of the two apps mentioned as example — Glassboard and Wunderlist — should use CloudKit.

And, since CloudKit is iOS and Mac only, and those two apps exist on other platforms, they couldn’t use CloudKit even if it did have private group data.

<a href="http://inessential.com/2014/06/08/notes_on_cloudkit">CloudKit is cool</a>, and I think lots of developers and users will benefit from it. But it’s important to set expectations properly, and not suggest that it’s useful in cases where it’s not.

(Hopefully that will change. I’d love for CloudKit to understand groups.)

Also, there’s this:

>Finally, CloudKit allows third-pa>rty apps to piggyback their authentication mechanism on Apple ID, thus making it easy to tell each user apart in a unique way without having to write and maintain a login system—and without forcing users to remember yet another password.

I don’t see how that’s true, either. If CloudKit gives you a user-specific token that identifies a user, sending that token to your own server — without an additional authentication system — isn’t secure. An attacker could submit random tokens until they found somebody’s data.

<i>Update a few minutes later:</i>

Kyle Sluder <a href="https://twitter.com/optshiftk/status/493791235455217664">asks on Twitter</a>:

>If authentication is user id + nonce, how is it not secure?

Good question. Perhaps this could be made to be secure.

So I’ll make another point: in the absence of Apple saying, “Yes, you can use it this way,” I wouldn’t. It feels like a misuse of the system, and something Apple would recommend against. Putting your app in that position is not a good idea, especially given that it’s the kind of practice Apple could choose to disallow.

If I’m wrong — if Apple is indeed offering just the authentication part of CloudKit as a service to developers — then I’d like to see where this is spelled-out.

<i>Update 9:45 am:</i>

Well, <a href="https://twitter.com/atomicbird/status/493797188955570176">Tom Harrington tells me</a> that Apple has indeed said you can use CloudKit authentication as a service.

>It was specifically mentioned in one of the CloudKit WWDC sessions. Log in with iCloud instead of Facebook or whatever.

That’s really cool. I’ll go back to the session and double-check, of course, but I don’t doubt Tom. (He knows this stuff.)

<i>Update 10:06 am:</i>

See <a href="http://inessential.com/2014/07/28/i_was_wrong_you_totally_can_use_cloudk">I Was Wrong — You Totally Can Use CloudKit for Identity</a>.
