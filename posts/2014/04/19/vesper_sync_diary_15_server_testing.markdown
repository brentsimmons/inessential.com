@title Vesper Sync Diary #15 - Server Testing
@pubDate 2014-04-19 18:15:11 -0700
@modDate 2014-04-19 18:15:11 -0700
I don’t write many tests as I go along, because I know  I’ll change the design and do a bunch of refactoring. Tests would have to be rewritten and rewritten again.

I *like* the idea of [test-driven development](http://en.wikipedia.org/wiki/Test-driven_development), but in practice it means more wasted time than I’d like. (For me. I’m sure it works great for other developers, but not every developer’s the same.)

I just ran cloc on the API server. It’s 1,545 lines of code. It’s small, which I take as a good thing. By the time I’ve finished writing tests it should be closer to 3,000 lines of code.


(If writing a Mac app is like writing a novel, and writing an iOS app is like writing a short story, then writing an API server is like writing a poem. It has to be compact, and every line has to have a reason to be there and has to do its job perfectly. In an iOS app you can slightly screw up an animation somewhere and just fix it later. On the server *nothing* can be slightly screwed up.)

#### My process

First step is to go through every single file and add all the easily-testable functions to a to-test list. That’s most of them.

As I’m going along I find some small refactorings that can be done that will make more things testable, so I jot those down and then do those after going through all the files. And update the list of functions to test.

Next step is to write the tests — using [Mocha](http://visionmedia.github.io/mocha/) — from the ground up. Do the low-level simple utility routines first.

(I used Josh Twist’s post on [unit testing Mobile Services scripts](http://www.thejoyofcode.com/Unit_testing_Mobile_Services_scripts_Day_7_.aspx) to help me get started.)

#### Live tests

Unit tests are indispensable, but there are two issues:

* They don’t actually hit the server itself.

* There are some things that are very difficult to test — because they need all the context of the server.

For instance, it’s easy to test the logic for merging notes, but it’s hard to test end-to-end — sending some notes to the server and making sure they really end up merged and stored in the database.

I’ve been thinking about what to do here and I don’t see any existing frameworks that fit the bill. ([Tell me](https://twitter.com/brentsimmons) if I’m wrong.)

So here’s my thinking. I’ll write code in the client app that calls the server and runs tests with some test data. Ideally these would be XCTestCase tests — with special junk for doing async tests — but if that doesn’t work, if it’s a special configuration of the app instead, I won’t stress about it. (Well. Weeeeell. I <em>might</em> stress about it. And bang on it until it works. Because it really ought to work. It bugs me so much that XCTestCase doesn’t have built-in support for async tests.)

This is made just a little more complex by the fact that I want to run tests against both the production and staging servers. That’s a small complexity, though. The bigger thing is the code to set up the environment on the server so that it can run the tests.

Here’s what I like, though: every line of code is testable. All the logic is testable. This is so different from client apps, where it’s hard-to-impossible to test everything.

Given the complete lack of margin for error, given my need to not constantly worry about the server, this is a wonderful thing.

PS I counted. First step is to write unit tests for 53 functions.
