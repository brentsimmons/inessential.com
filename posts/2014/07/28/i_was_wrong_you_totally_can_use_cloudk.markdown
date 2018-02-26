@title I Was Wrong — You Totally Can Use CloudKit for Identity
@pubDate 2014-07-28 10:06:05 -0700
@modDate 2014-07-28 10:08:59 -0700
See Session 208, Introducing CloudKit.

Your app gets a stable but random user identifier that does not include any user information. Two different applications get different identifiers, but the same application run by the same user on different devices get the same identifier, as you’d expect.

From the session, at 40:36:

>And lastly, this is an independent API. This is a section of the CloudKit framework. You can use this in collaboration with the database API, or you can use this completely separately. We’ve given you enough support that, if you wanted to, you could implement a login-via-iCloud flow in your application using the CloudKit framework.
