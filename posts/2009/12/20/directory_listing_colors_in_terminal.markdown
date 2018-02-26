@title Directory listing colors in Terminal
@pubDate Sun Dec 20 13:24:31 -0800 2009
@modDate Sun Dec 20 13:24:31 -0800 2009
I like to have colors in my directory listings when in Terminal. Blue for folders, red for executable, etc. I’ve been doing this for years, and I always forget it’s not the default.

I use tcsh (still, yes), so I have the following in my .tcsh file:

<code>setenv LSCOLORS "exfxcxdxbxegedabagacad"</code>

Gibbery, yes. But it specifies colors for <code>ls</code> listings.

If you use bash, the following in .bash_profile should work:

<code>export LSCOLORS="exfxcxdxbxegedabagacad"</code>

(Remember to do a <code>source .tcsh</code> or <code>source .bash_profile</code> after editing the file.)

If it doesn’t work, you might still have to set CLICOLOR to true, and possibly set TERM to xterm-color.

And of course you can change the colors — do a <code>man ls</code> for more info.
