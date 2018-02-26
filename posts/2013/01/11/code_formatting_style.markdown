@title Code Formatting Style
@pubDate Fri Jan 11 12:09:16 -0800 2013
@modDate Fri Jan 11 12:12:55 -0800 2013
On the <a href="http://www.imore.com/debug-5-craig-hockenberry-sean-heber-and-twitterrific">Debug podcast</a> (which I adore), <a href="http://furbo.org">Craig Hockenberry</a> (whom I adore) mentioned that my code formatting style is crazy.

He may be right. I’ll let you judge.

Here’s a simple example from a view controller’s init method:

<code>- (id)initWithAccount:(GBAccount *)account {<br />
 <br />	
&nbsp;&nbsp;&nbsp;&nbsp;self = [self initWithNibName:@"Settings\_iPhone" bundle:nil];<br />
&nbsp;&nbsp;&nbsp;&nbsp;if (self == nil)<br />
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return nil;<br />
 <br />	
&nbsp;&nbsp;&nbsp;&nbsp;_account = account;<br />
&nbsp;&nbsp;&nbsp;&nbsp;return self;<br />
}</code>

My formatting style is pretty much <a href="http://en.wikipedia.org/wiki/Indent_style#K.26R_style">K&R style</a>, plucked straight from the C Programming Book — with one modification: opening braces for methods and functions appear at the end of the line rather than on the next line.

With K&R style, you put the opening brace at the end of the line for other blocks (if, while, etc.) — but not with functions. I prefer the more consistent approach of putting the brace at the end of the line for <em>all</em> blocks.

You might not agree with its readability — but I find it cleaner and easier to scan my style than this:

<code>- (id)initWithAccount:(GBAccount *)account<br />
{<br />	
&nbsp;&nbsp;&nbsp;&nbsp;self = [self initWithNibName:@"Settings\_iPhone" bundle:nil];<br />
&nbsp;&nbsp;&nbsp;&nbsp;if (self == nil)<br />
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return nil;<br />
 <br />	
&nbsp;&nbsp;&nbsp;&nbsp;_account = account;<br />
&nbsp;&nbsp;&nbsp;&nbsp;return self;<br />
}</code>

And much easier than this:

<code>- (id)initWithAccount:(GBAccount *)account<br />
{<br />	
&nbsp;&nbsp;&nbsp;&nbsp;self = [self initWithNibName:@"Settings\_iPhone" bundle:nil];<br />
&nbsp;&nbsp;&nbsp;&nbsp;if (self == nil)<br />
&nbsp;&nbsp;&nbsp;&nbsp;{<br />
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return nil;<br />
&nbsp;&nbsp;&nbsp;&nbsp;}<br />
 <br />	
&nbsp;&nbsp;&nbsp;&nbsp;_account = account;<br />
&nbsp;&nbsp;&nbsp;&nbsp;return self;<br />
}</code>

Or this:

<code>- (id)initWithAccount:(GBAccount *)account<br />
{<br />	
&nbsp;&nbsp;&nbsp;&nbsp;self = [self initWithNibName:@"Settings\_iPhone" bundle:nil];<br />
&nbsp;&nbsp;&nbsp;&nbsp;if (self != nil)<br />
&nbsp;&nbsp;&nbsp;&nbsp;{<br />
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_account = account;<br />
&nbsp;&nbsp;&nbsp;&nbsp;}<br />
 <br />	
&nbsp;&nbsp;&nbsp;&nbsp;return self;<br />
}</code>

It’s a matter of what you’re used to, I think — I don’t for one second contend that there are right and wrong ways. There aren’t. Consistency matters more, because any reasonable style is readable and scannable as long as it’s consistent.
