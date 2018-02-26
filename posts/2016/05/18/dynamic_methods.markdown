@title 0.0001% of the Way to Core Data
@pubDate 2016-05-18 13:20:51 -0700
@modDate 2016-05-18 19:25:13 -0700
This post isn’t about Core Data — but it’s a well-known example of adding methods at runtime, so I’ll use it.

Let’s imagine you want to make something like Core Data. You have a bunch of different model objects backed by a database. You want to implement faulting — that is, an object’s properties are nil in memory until you actually access one of the properties, at which point it pulls its values from the database.

You have some options for how to do this. You could skip properties entirely and override `valueForKey:` and `setValue:forKey:`, and always access the values that way. Your overridden versions of those two methods would handle faulting. But this makes for a bunch of strings in your code, and it isn’t nearly as readable as `obj.foo = bar`.

Alternately you could create all the getters and setters by hand, for all the properties in all your data objects, and be sure to include a hypothetical `fetchIfNeeded` call in every single getter and setter. That’s a ton of copy-and-pasting. It gets you `obj.foo = bar` syntax, but it’s also tedious, error-prone, and painful to maintain. (You could use macros or a script to make this a bit easier, but it’s still sucky.)

Instead, you want to solve the problem reliably and once. You want maintenance of your data objects to be no more difficult than adding and removing properties and their associated `@dynamic` declarations. (Actual database schema maintenance is a separate consideration — that’s in the remaining 99.9999% of the way to Core Data.)

While I can’t say for sure how Core Data adds methods at runtime, I can say for sure that this particular magic is available to us and not just to Apple. Which is as it should be — we have every right to expect that same power.

#### How to add methods at runtime

Here’s the plan. We’ll create a `DataObject` class that adds methods. Your model classes will inherit from `DataObject`. Your model classes will be free of anything odd — all that stuff goes into `DataObject`, which you can write once and then forget.

You need a class method — <code>+ (BOOL)resolveInstanceMethod:(SEL)selector</code> — that will get called when the runtime is looking for the accessors for your properties.

If the selector is a getter or setter for one of your properties, then your `resolveInstanceMethod` will call `class_addMethod`, which appears in objc/runtime.h, with the appropriate parameters, including a C function that is the actual implementation of the method (an IMP).

Example: <code>class_addMethod(&#8203;[self class], selector, (IMP)getterIMP, "@@:");</code>

It’s actually unbelievably easy. See my [sample demo app on Bitbucket](https://bitbucket.org/brentsimmons/dynamicproperties/src/), which shows the basics.

(You can get fancier than I did — you might start by using reflection to get the list of property names instead of using an array, for instance. You could handle non-object types.)

#### But why?

Maybe you’re thinking, “Great, but I already just use Core Data and don’t need this at all.”

First: congratulations on using Core Data. It’s the right move.

Second: imagine a different scenario — think of [DB5](https://github.com/quartermaster/DB5). DB5 lets you put a bunch of appearance definitions — strings, colors, edge insets, and so on — inside a plist so that you don’t have to scatter all these values throughout your app. It’s a nice utility, but its API is all string-based, which means plenty of room for typos and errors.

Imagine, instead, if you could define the set of appearance properties your app needs. This would make errors less likely: the compiler would be your friend. But you definitely don’t want to go through the error-prone work of actually creating a hundred accessors — you want those created automatically for you at runtime.

As you might imagine, someone’s actually already done that: it’s how Omni’s OAAppearance class works. And, as a bonus, there’s an [Xcoders talk from Curt Clifton](https://vimeo.com/151482623) that goes into detail. (The audio isn’t great, but the talk is worth it anyway.)

And, as a double-bonus, [OAAppearance is open source](https://github.com/omnigroup/OmniGroup/tree/master/Frameworks/OmniAppKit/Appearance) on GitHub.
