@title Super-simple Xcode user script for header files
@pubDate Thu Feb 26 12:50:24 -0800 2009
@modDate Thu Feb 26 13:26:46 -0800 2009
Sometimes a little naggy thing can be solved really, really easily.

Here’s the thing:

I usually create my methods in my .m file, then decide if I want to copy and paste the top line into the .h file.

If I do, then I have the issue where I’ve copied something like this...

	- (void)someMethod {

...but I want the following in the .h file:

	- (void)someMethod;

I wrote a little Xcode user script to deal with this. I gave it a cmd-{ keystroke. I find that I use it <em>all the time</em>.

The incredibly simple script looks like this:

	#!/usr/bin/env ruby
	s = STDIN.read
	s.gsub!(" {\n", ";\n")
	print s

The way it works: I copy from the .m file, hit cmd-option-upArrow to go to the .h file, paste, select the line (shift-upArrow, since the cursor is on the line immediately below), then hit cmd-{ to run the script. Saves me from manually changing the { to ;.

It’s safe to run over multiple lines, too.

That’s still too many steps, by the way — I’d really love to be able select the line in the .m file, then hit a keyboard shortcut to insert it in the .h file at the end of the list. But I haven’t gotten that far yet. (Though <a href="http://cocoawithlove.com/2008/12/instance-variable-to-synthesized.html">this page on Cocoa with Love</a> might provide some good tips.)

Update: I’m fully aware that both of the following are legal in .m files...

	- (void)someMethod; {

	- (void)someMethod;
	{

...but, no offense to Andrew Stone (who I first saw <a href="http://www.stone.com/The_Cocoa_Files/Writing_Good_Cocoa_Code.html">write about this</a>), I don’t like it. The ; is unneccessary, and I’m compelled to delete it. I know myself — I will never, ever, ever allow that extra ; to sit there. I don’t think I could even sleep, knowing there are lovely little semicolons to delete.
