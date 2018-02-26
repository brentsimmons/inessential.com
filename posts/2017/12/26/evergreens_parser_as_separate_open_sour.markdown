@title Evergreen’s Parser as Separate Open Source Framework
@pubDate 2017-12-26 18:10:09 -0800
@modDate 2017-12-26 18:10:09 -0800
I copied Evergreen’s parsing framework, RSParser, to a <a href="https://github.com/brentsimmons/RSParser">separate repository on GitHub</a>.

It has no dependencies other than system-supplied libraries. It’s offered via the MIT License.

It builds a Mac framework only at the moment, but adding an iOS target should be easy. It’s the one issue in the bug tracker (at least so far).

Otherwise it’s fast and stable and does the jobs it’s designed to do.

#### Things it parses

* RSS
* Atom
* JSON Feed
* RSS-in-JSON
* OPML
* Internet dates
* HTML metadata
* HTML links

In addition, you can build your own XML or HTML parser by creating an `RSSAXParserDelegate` or `RSSAXHTMLParserDelegate`.

It’s a mix of Objective-C and Swift. More recent code is in Swift.

Parsing a feed that’s RSS, Atom, JSON Feed, or RSS-in-JSON is a matter of calling `FeedParser.parse` and getting back a `ParsedFeed` object. Pretty simple.
