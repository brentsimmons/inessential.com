@title Swift Diary #4: KVC Again
@pubDate 2015-07-24 10:04:45 -0700
@modDate 2015-07-24 10:10:12 -0700
Al Skipp <a href="https://twitter.com/al_skipp/status/624549746640834560">wisely writes</a> (in reply to <a href="http://inessential.com/2015/07/22/swift_diary_2_kvc">my post about KVC</a>):

>It's still the case that Stringly typed code is a pain in the Aris to write/debug/maintain.

True. So true.

But let me remind you of a place where most iOS and Mac developers do it all the time: Interface Builder.

#### Interface Builder is a Very Fancy XML Editor

Some developers eschew Interface Builder (IB) altogether. That’s fair. I myself don’t automatically reach for it — there are times when a UI is so simple that it doesn’t need it, or it’s too dynamic to be expressed well in IB. So I at least think about it before I go there. But I do use it plenty often.

And I’d bet that most developers use IB at least a little bit, if not a lot, in their apps. (Though maybe not for games.)

And what you do you do in IB? You type (or copy-and-paste) in the class name of your view controller. You click checkboxes and set attributes. In the end you’re just setting a bunch of strings that gets stored in an XML file.

In the end, you get things like this:

<code>&lt;buttonCell key="cell" type="square" bezelStyle="shadowlessSquare" image="gear" imagePosition="only" alignment="center" borderStyle="border" inset="2" id="1194" customClass="TransparentButtonCell"&gt;</code>

You don’t want to do edit that directly, of course, so you have IB. But this is still what you end up with.

#### Runtime

<a href="https://twitter.com/gparker/status/1787428084">Nib loading uses KVC</a>. Though it may not use <code>setValue:forKey:</code> directly, it does the conceptual equivalent.

That does not mean that you can only interact with your objects via <code>valueForKey:</code> and <code>setValue:forKey:</code>, of course. It’s just that instantiating uses KVC. Your own code is still <code>foo.bar = 7</code> and so on.

The alternative to KVC (or something much like it) — commence shuddering now — would be *code generation* instead. (Those of you who’ve been through that on other platforms, come out from under your desk. It’ll be okay.)

#### Trade-offs

Of course, it *is* a pain when you’ve mistyped — or just plain forgot to type — the name of a class in IB. That’s a drawback of any system like this.

But we’re willing to make the trade-off because the productivity gain we get from using IB is worth the occasional issue like this. The nice thing about bugs like that is that they’re usually caught very quickly, and are just a normal part of the development process. It’s what we do for a living.

#### If IB can do it, why can’t I?

It’s a pretty nice system. I get to declare things rather than write code — and though I have to take care that my declarations are correct, I still end up saving time and writing and maintaining less code. It’s a win.

The Core Data modeler is another example. I don’t have a handy example, but I bet it generates XML (or maybe JSON or, more likely, plists). And the runtime uses KVC and KVO (and method generation, which is another topic) to make it all work.

It’s only natural that I might want to write similar systems for my own use. And I have. In the case of the database and model object code that I’ve written, I don’t have a fancy modeler — I just edit a plist. Though editing is more raw, the concept is the same: I type in class names and map database columns to types and property names.

And my code — which I can reuse unchanged in as many apps as I want to — uses KVC to put it all together. As IB does.

The *rest* of my code — the code outside my database code — doesn’t use KVC. I still write <code>foo.bar = 7</code>, rather than <code>[foo setValue:@7 forKey:@"bar"]</code>. I can rely on the compiler to tell me when I’ve made an error in the rest of my code.

So, in the end, this stringly-typed database/model-object code is way *less* of a pain to write, debug, and maintain.

In fact, I don’t touch it at all, since it’s debugged and working.

But I’d still love to make it work with pure Swift objects and structs.
