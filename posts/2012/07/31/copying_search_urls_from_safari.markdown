@title Copying Search URLs from Safari
@pubDate Tue Jul 31 21:47:08 -0700 2012
@modDate Tue Jul 31 23:45:40 -0700 2012
I upgraded to Mountain Lion on my laptop. (But not on my desktop development machine yet, just due to healthy pre-shipping-paranoia.)

I wasn’t sure what I’d think of the new combined address/search bar in Safari. I’m skeptical when software tries too hard to divine my intentions. Past experience has shown me that software often gets it wrong, and it becomes very difficult to make it do what I want.

But — at least so far — I’ve been happy with the new address/search bar. It *does* figure out what I want to do.

I did find an unexpected problem, though: I wanted to give somebody else the URL of a Google search I just did. And I couldn’t.

<img src="http://inessential.com/images/safari_search_copy_link.png" alt="Screenshot showing Safari’s search/address bar" width="299" height="35" />

I asked on Twitter. One way is to drag the magnifying glass into whatever text I’m editing. Another way would be a <a href="https://twitter.com/pwc/status/230514299104280576">bookmarklet</a> that gets the current page location. A third way would be an <a href="https://twitter.com/cocoadog/status/230520088430784513">AppleScript script</a>.

I ended up writing a <a href="https://gist.github.com/3223686">Python script</a>.

<script src="https://gist.github.com/3223686.js?file=googleSearchString.py"></script>

Now I can just switch to Terminal (cmd-escape on my machine, thanks to <a href="http://www.red-sweater.com/fastscripts/">FastScripts</a>), start typing the name of the script, hit Tab, then paste in my search results. (No need even to put them in quotes.) Hit return, and then a search string is on the clipboard.

So it’s not that bad. At least for someone like me who’s only a split-second away from the Terminal at all times. But it’s not nearly as nice as just copying the URL out of the address bar.

It’s *weird* that the address bar doesn’t always include an address. It feels like a contract has been broken. Maybe it’s one that needed to be broken. (And maybe not.)

<i>Update 11:30 pm</i>: I like <a href="https://twitter.com/porada/status/230547056610136064">Andy Lee’s script and Dominik Porada’s additions</a>.
