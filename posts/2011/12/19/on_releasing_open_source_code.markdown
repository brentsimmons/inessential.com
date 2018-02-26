@title On Releasing Open Source Code
@pubDate Mon Dec 19 10:55:52 -0800 2011
@modDate Mon Dec 19 10:55:52 -0800 2011
Matt Gemmell: <a href="http://mattgemmell.com/2011/12/19/open-source-code/">Open Source Code</a>.

>I strongly encourage releasing reusable portions of your code - it’s the lifeblood of the developer community. Over the years, I’ve put together a set of best practices for releasing open source code, to make life easier partly for yourself but mainly for those who will use your code.

To his excellent article I’d add the following specifically for Cocoa developers:

- Make sure the static analyzer shows no issues with your code.
- Turn on the same <a href="http://boredzo.org/blog/archives/2009-11-07/warnings">warnings that Peter Hosey uses</a>, and make sure there are no warnings.
- Use ARC.
