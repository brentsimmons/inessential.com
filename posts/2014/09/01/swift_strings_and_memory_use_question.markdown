@title Swift, Strings, and Memory Use Question
@pubDate 2014-09-01 14:04:30 -0700
@modDate 2014-09-01 20:46:11 -0700
Do I understand this correctly? NSString (usually) stores strings in memory as UTF-16, while Swift uses UTF-8. Correct?

If so, then I think this means that for text-heavy apps — such as Vesper, such as RSS readers and Twitter clients and similar — there could be a nice reduction in memory use due to this change. (If they use Swift strings.)

True?

<i>Update a few minutes later:</i> <a href="https://twitter.com/al45tair/status/506550812257296384">Alastair Houghton tweets</a>:

>No. NSString stores strings as 8-bit ASCII where possible. It only uses UTF-16 if it has to

<i>Update 8:40 pm:</i> Well, maybe. Sometimes. Consider the many European languages that have accented characters — those aren’t ASCII characters, which means NSString would use UTF-16. But if Swift uses UTF-8 in those cases, then it should save memory, since not all (or even most) of the characters are accented.

Or, as <a href="https://twitter.com/al45tair/status/506554668647215106">Alastair Houghton tweeted</a> when I asked him about this case:

>Yes, e.g. in European languages (French, German, Spanish etc) where many chars are ASCII but some are accented.

(Also remember that words with accented characters — résumé, éclair — appear in written American English too.)
