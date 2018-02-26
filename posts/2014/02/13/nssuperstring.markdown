@title NSSuperString
@link http://www.objc.io/issue-9/
@pubDate 2014-02-13 12:26:50 -0800
@modDate 2014-02-13 15:07:01 -0800
[objc.io issue #9](http://www.objc.io/issue-9/) is a great reminder of how incredibly awesome NSString is.

I’m not saying we never have to think about Unicode, but it’s pretty darn close.

Consider JavaScript. Will s.length return what you expect? [Not always](http://mathiasbynens.be/notes/javascript-unicode). ('💩'.length returns 2.)

Or [consider Go strings](http://blog.golang.org/strings) (Go is an interesting language worth learning about):

>Strings are built from bytes so indexing them yields bytes, not characters. A string might not even hold characters. In fact, the definition of “character” is ambiguous and it would be a mistake to try to resolve the ambiguity by defining that strings are made of characters.

I’m sure there are good reasons for Go’s string design, but I strongly prefer NSString’s collection of characters rather than bytes.

<i>Update 3:04 pm</i>: Or maybe I’m wrong about all this! NSString also returns 2 for [@"💩" length].

Well, I stand by NSString being great. But, darn, I thought it had this stuff a little bit more nailed than it apparently does.
