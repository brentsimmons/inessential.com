@title Security bug?
@pubDate Tue Feb 19 17:15:06 -0800 2013
@modDate Tue Feb 19 18:06:54 -0800 2013
When Twitter was recently hacked, I was among those who got an email saying I was affected. So I changed my password.

But here’s what I’ve noticed: changing my password does *not* cause any of the Twitter clients on my iPhone to ask me again for authentication. They just keep working normally.

So here’s the scenario I worry about. I don’t know if this is accurate or not, or if it applies only to Twitter or is a more general OAuth issue.

1. Somebody gets my Twitter password.

2. They login using the same client I use, but on their iPhone. The client starts working.

3. I change my password.

4. They’re unaffected — that client continues to work on their iPhone, just as it does on mine.

Is this true?

If so, I don’t like it.

#### Update 5:50 pm

I should say what bothers me.

Yes, I can go into my Twitter settings and revoke access to any one or more apps. And: I’m a developer, and I’ve written OAuth client code — I’ve even written Twitter-specific code.

But here’s what normal people think: <em>I’ll change my password and everything will be okay</em>.

And I admit to having changed my password recently and been surprised that my Twitter client kept working, even though I should have known that it would keep working (had I thought about it).

Here’s the first paragraph of that email Twitter sent to a bunch of folks a couple weeks ago:

>Twitter believes that your account may have been compromised by a website or service not associated with Twitter. We've reset your password to prevent others from accessing your account.

Which would lead a normal person to believe that resetting your password would prevent other people from accessing your account in any way. But it’s not true, not if they’ve already accessed your account.

That email also says, near the end:

>Review your approved connections on your Applications page at https://twitter.com/settings/applications. If you see any applications that you don't recognize, click the Revoke Access button.

That’s good advice. However, if somebody else is using the very same client I use, or a client I used previously, I won’t see any apps I don’t recognize. (It could be a long list of apps, all recognized.)

I understand that OAuth is a security win in some ways. But implementors should, I think, be mindful of what normal people expect — which is that changing your password locks out every app until you re-authenticate.
