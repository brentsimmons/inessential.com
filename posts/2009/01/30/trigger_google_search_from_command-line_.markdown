@title Trigger Google search from command line script
@pubDate Fri Jan 30 10:50:23 -0800 2009
@modDate Fri Jan 30 10:51:03 -0800 2009
I did actually write one small Python script, which I probably use a dozen times a day. It lets me trigger a Google search from the command line.

In Terminal I just type something like <code>gs bacon</code> or <code>gs 'shakespeare globe'</code>. The search results page then opens in my browser.

Here’s the <em>very</em> simple script:

<code>#!/usr/bin/python</code>

<code>import sys<br />
import os<br />
from urllib import urlencode</code>

<code>os.system("open " + "http://www.google.com/search?" + urlencode({'q':sys.argv[1]}))</code>

(Note: the last line that begins with <code>os.system</code> should be all just one line.)
