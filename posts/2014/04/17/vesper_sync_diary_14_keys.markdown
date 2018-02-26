@title Vesper Sync Diary #14 - Keys
@pubDate 2014-04-17 10:52:03 -0700
@modDate 2014-04-17 10:52:03 -0700
Here’s the initial design: the text of notes is encrypted in the database. The key is not stored in the source code. (The source code could get out and you wouldn’t be able to decrypt notes.)

That design is a no-brainer, and I thought I was finished at that point. But then I did a design review with some security folks, and they suggested I revise it like this:

The text of notes is encrypted in the database. They key is not stored in the source code. The key should *change* from time to time. To make this work:

* Always encrypt using the latest key.

* Add some token to the text that lets me know if it’s been successfully decrypted.

* Try decrypting using the latest key first. If the token doesn’t appear in the right place, use the previous key. Repeat if necessary until decrypted.

* Add a new key regularly. (Twice a year, for example.)

* Be prepared with a script that re-encrypts all note text with the latest key, in case there are any security concerns at all.

This is sensible. I can’t think of any reason not to do it this way. Is there anything I’m missing?
