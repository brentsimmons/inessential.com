@title Extracting Links
@pubDate 2014-02-08 15:38:52 -0800
@modDate 2014-02-08 15:38:52 -0800
Justin Williams wrote about a [hanging bug in Glassboard](http://carpeaqua.com/2014/02/08/adventures-in-debugging-nsregularexpression-edition/) that could happen when pulling links from a string using a regular expression.

We’re using a newer regular expression in Vesper that fixes this bug.

John has [published it as a gist](http://daringfireball.net/linked/2014/02/08/improved-improved-regex) and we’ve [added it to QSKit](https://github.com/quartermaster/QSKit/blob/master/Classes/Foundation/NSString%2BQSKit.m).

Our tests [include Justin’s tests](https://github.com/quartermaster/QSKit/blob/master/QSKitTests/NSStringTests.m). It passes.
