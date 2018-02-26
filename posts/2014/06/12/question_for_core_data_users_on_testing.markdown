@title Question for Core Data Users on Testing
@pubDate 2014-06-12 11:12:31 -0700
@modDate 2014-06-12 11:16:28 -0700
I’m exercising some measure of self-discipline and writing more tests (for both iOS app and server) before I allow myself to make any potentially breaking changes. (I’d rather be writing Swift code for my Mac app. But it can wait.)

One of the things I’m testing is JSON serialization and de-serialization for VSTag and VSNote objects.

I wondered how you’d do this in Core Data. I’m asking earnestly, because I don’t know and I’d like to know, because I strongly suspect (contra the opinion of everybody who knows me) that I’ll be using Core Data some day.

Here’s what I do right now:

* Alloc/init a VSTag object. Set some properties.

* Get a dictionary from its JSONRepresentation method.

* XCTAssert that the values in the dictionary are as expected.

(The process for the reverse is as expected. Create dictionary, call the method that creates a VSTag object with the dictionary, then XCTAssert that the VSTag’s properties are as expected.)

Note that I don’t have to set up a Core Data stack. The VSTag object doesn’t get saved anywhere. It’s just a plain old object that goes away at the end of the test, without persisting.

If you’re using Core Data, what do you do for these kinds of tests where you need model objects but you don’t want to save them?

<i>Update:</i> the answer [comes from Colin Cornaby](https://twitter.com/colincornaby/status/477152066612113409):

>Create a special test store, save there. Also tests your schema validation. Or use in memory store.
