@title IBAction vs. void
@pubDate 2014-02-09 14:50:00 -0800
@modDate 2014-02-09 16:12:24 -0800
This issue came up in private correspondence. Should you always use `IBAction` for actions? Is there some advantage to using `void` instead? Or the other way around?

Here’s my thinking:

I use `IBAction` for the sole case where the action is directly wired up in Interface Builder. It’s a reminder that there’s a xib or storyboard and this action is called directly with this target.

Otherwise I use `void`.

In both cases I put the actions in a `#pragma mark - Actions` section of the code. And I always use the form `- (void)someAction:(id)sender`. (That is, I always include `sender`, which is a further clue that it’s an action method.)

Also, I almost never wire up actions to an explicit target in Interface Builder. Instead I use the [responder chain](https://developer.apple.com/library/ios/documentation/EventHandling/Conceptual/EventHandlingiPhoneOS/event_delivery_responder_chain/event_delivery_responder_chain.html), even on iOS apps — meaning that I wire actions to First Responder. (If you’re an iOS developer and you’re not up on the responder chain, you’re missing out. It’s important.)

This has the effect of making `IBAction` pretty rare in my code. It doesn’t appear at all in the current shipping version of Vesper.

#### Update 4 p.m.

Some unstated things, and a good reason to use IBAction:

I don’t use IB that much (though I’m trying to fix that, when possible). But when I do, I add a method to First Responder, then wire up the action to First Responder.

However, if I already had an action method with the `IBAction` macro, then I could wire it up to First Responder without having to add the method in IB. Totally true. (And that’s a good reason to disagree with me.)

Here’s why I do it this way: I usually do IB first, code second. There may not be an action method or even a view controller when I’m in IB. Since I usually do things this way (when I do use IB), it makes sense to me to always do it the same way.

Another reason is that because I don’t use IB that often, most of the time when I’m setting up actions I’m doing so programatically, with a nil target and a selector. There’s absolutely no need for `IBAction` when doing it this way, and I’m far out of the habit of using it.

In the end, my main reason is still the important one: I like to use `IBAction` as an indicator that an action is explicitly wired to this specific target. It doesn’t have to mean that, but I like it to mean that.

But you may agree with [Wil Shipley](https://twitter.com/wilshipley/status/432661316101099520):

>Seems like a lot of work to avoid IBAction.
