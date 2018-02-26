@title Strange Dialect
@pubDate 2014-03-11 10:21:24 -0700
@modDate 2014-03-11 13:00:23 -0700
[Nicolas Bouilleaud](https://twitter.com/_nb/status/443313514716098560) linked to the [WebScript programming guide](https://developer.apple.com/legacy/library/documentation/LegacyTechnologies/WebObjects/WebObjects_3.1/PDF/DEVGUIDE/SCRIPT.PDF).

I never worked with WebScript (or WebObjects), but I find this document fascinating.

Types are not permitted — everything’s an `id`. There is a literal syntax for arrays and dictionaries, but only constants are permitted. And the syntax is a little different. Example: <code>myDictionary = @{"key" = 16};</code>.

Selectors are just quoted, as in <code>selector:"timeOfSession"</code>.

About halfway-through there’s a section about “Modern” WebScript Syntax. (“Modern” is quoted in the original.) It’s “a variation of WebScript designed to appeal to programmers more familiar with such languages as Visual Basic and Java.” It’s weird. (To you and me.)

It does make me think — which I’ve thought before — that there’s a scripting language living inside Objective-C just waiting to get out. And then I remember that [JSTalk is pretty darn close](http://jstalk.org//).
