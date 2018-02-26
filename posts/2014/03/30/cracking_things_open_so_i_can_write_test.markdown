@title Cracking Things Open So I Can Write Tests
@pubDate 2014-03-30 12:26:19 -0700
@modDate 2014-03-31 09:26:42 -0700
Though [Q Branch Standard Kit](https://github.com/quartermaster/QSKit) has a bunch of tests, Vesper doesn’t. I’ve never been very good about automated tests for my apps.

I’m changing that right now. The next version of Vesper will be very well-tested — mainly because I need to make sure every aspect of syncing has been tested thoroughly.

I’ve been bad about testing in the past because so many things are hard to test. Or they’re so obvious that a quick human test is the best thing. Or they require a great deal of state. Does that animation look right? Does the browser open when you tap a link? Does that thing popup after you type two characters? Etc.

(That’s not to say that automated UI testing isn’t do-able. [It is](http://alexvollmer.com/posts/2010/07/03/working-with-uiautomation/). But it’s more that I haven’t even gotten that far. I should do regular testing first.)

#### Initial Victory

I had a nice class with an ugly name — VSV1DataMigrater — that did what you think: it took a Vesper 1.x database and migrated the data to a Vesper 2.x database. Then it moved the old database to a new location so the migration wouldn’t happen twice.

I couldn’t figure out how to test this. It did a bunch of async stuff. It wanted some databases to be in the right place in the file system. The migration would run automatically at app startup anyway, since the database would have to be in the right location — which means the test wouldn’t run because the database would get moved before the test got a chance to run.

After some futzing, I finally asked myself what part of this I really needed to test. Answer: data extraction. I want to make sure that the objects generated from the old database were what I expected. That is: notes have the right text, tags, attachments, and so on.

So I took a hammer to this class and broke out a VSV1DataExtracter class. (Another ugly name, but accurate.) It takes an FMDatabase and returns the extracted model objects, and doesn’t do anything else.

Since it takes that parameter, I can use a test database stored anywhere (rather than where the app expects it). I added a test database to the Vesper Tests target.

Since it has no notion of a queue — but can be called from within a queue, and will be when running normally — I could call it from the main thread, so I don’t have to deal with async XCTests. (Which looks like a pain. I expect I’ll have to go there soon.)

I consider this a case where the needs of testing made for better code. [It’s good](https://www.youtube.com/watch?v=AkJcFGvNgcY) that the data extracter is its own class that takes a parameter and runs without side effects of any kind.

#### Next Up: VSTagSuggestionView

Here’s a case I’m not sure how to handle.

The tag suggestion view (which appears as you’re typing a tag) searches through the list of tags using some NSPredicates. It’s a single method in VSTagSuggestionView — but it’s obviously the kind of thing that can and should be tested.

The method looks like this:

<code>- (NSArray \*)tagsMatchingSearchString:(NSString \*)searchString;</code>

It asks the data layer for all tags that have at least one note, then runs the predicates on those tags and returns an array of matching tags.

The first thing to do is obvious: it should take an array of tags as a parameter, so tests don’t rely on the state of the database. I’d change the method to look like this:

<code>- (NSArray \*)tags:(NSArray \*)tags matchingSearchString:(NSString \*)searchString;</code>

But here’s where I’m not sure of the best thing to do.

I could leave the method in VSTagSuggestionView, where it belongs (nowhere else is this method needed). But that means that to test it I have to add the method to VSTagSuggestionView.h so a test method can see it. It also means that a test method needs to instantiate a VSTagSuggestionView.

I could fix the second problem by making it a class method. But that still leaves this method in the .h file, where it would exist solely for the purpose of testing. I don’t like that.

Or I could make it a separate class — but it seems crazy to do that for one pretty simple method that’s used in just one place. (I’d be on the way to creating testing bunnies.)

What do experienced testers do in this case?

<i>Update 2:15 pm</i>: [Lots of good advice via Twitter](https://twitter.com/brentsimmons/status/450354765013082112). (Email too.)

Here’s what I decided for this case: I created a VSTagSuggester class. It has one method which can be directly tested:

<code>+ (NSArray \*)tags:(NSArray \*)tags matchingSearchString:(NSString \*)searchString;</code>

I could worry about creating a zillion of these and ending up with test bunnies. But so far it’s just one of these objects, so I’ll keep calm.
