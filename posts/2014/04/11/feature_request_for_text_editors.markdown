@title Feature Request for Text Editors
@pubDate 2014-04-11 21:09:42 -0700
@modDate 2014-04-11 21:09:42 -0700
(Maybe there’s a text editor that does this that I don’t know about. But I haven’t found one.)

I have my Node.js project open in my text editor. Folders and files are in the left-hand sidebar. Click on one to show that file. You know the picture.

(Wouldn’t have to be Node.js. Could be any programming project.)

Now I’m looking at a file that references a function that I want to look up. As an Xcode user, I expect to be able to cmd-click on the name and go right there, even if it’s in another file. And then I expect to be able to go right back to where I was with a keyboard shortcut. (Or with a swipe on my mouse.)

But it doesn’t work. The text editor is smart enough to be able to give me a list of the symbols in each file, but it’s not putting this all together.

I’ve made this work before — at least the navigate-to-symbol part — by maintaining a <a href="http://en.wikipedia.org/wiki/Ctags">Ctags file</a>. But this is a pain. It needs to be updated when things change.

What I want is the obvious thing: the text editor — which knows what language each file is, which knows where the root folder is — should handle creating and updating the Ctags file behind the scenes. It should do this for me.

And the second part of this — going back easily — is just as critical.

My point: a significant chunk of programming is just *navigating*, and no text editors (that I know of) get this completely.

It should work like a browser. Forward and back.

(For bonus points: it’s not file-based but based on position in file. Say I’m at line 300, and I go to the top of the file to include another file. I want to jump back to line 300 the same way I’d go back to a separate file.)

If there *is* a text editor that does this — all of this — <a href="https://twitter.com/brentsimmons">let me know</a> what it is because I want it right now.
