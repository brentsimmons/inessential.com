@title Accessibility and the Dynamic Nature of Objective-C
@pubDate 2020-07-01 21:48:00 -0700
@modDate 2020-07-01 21:48:00 -0700
Doug Russell, who used to work on accessibility at Apple, [writes](http://www.takingnotes.co/blog/2020/07/01/accessibility-engineering/):

> some of the code that powers accessibility on apple platforms is just disgusting to look at and to work on.
>
> most of the code that makes apple software accessible lives in what’s called an accessibility bundle. without diving into the minutia of the thing, bundles are a way to load something akin to a plugin into a cocoa app at runtime if an assistive technology is activated. it involves manipulating the app or framework class hierarchy and using objective-c dynamism to read app state and build up a usable accessibility hierarchy. insert a super class here, read an instance variable there, swizzle in a method and store the state for it in associated objects.

In other words — Objective-C and its runtime play a big role in making Apple’s great accessibility possible.

What happens when that’s not really a thing anymore?
