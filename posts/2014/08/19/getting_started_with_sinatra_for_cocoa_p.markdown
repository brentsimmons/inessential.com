@title Getting Started with Sinatra for Cocoa Programmers
@pubDate 2014-08-19 09:59:14 -0700
@modDate 2014-08-19 09:59:14 -0700
<a href="http://www.sinatrarb.com/">Sinatra</a> is the little brother to <a href="http://rubyonrails.org">Ruby on Rails</a>.

You’d think that a Cocoa guy like me — someone who’s quite happy working with a large application framework — would prefer Rails, but I find myself attracted to the smaller and lighter-weight Sinatra.

Sinatra and <a href="http://nodejs.org">Node</a> are very similar. But as awesome as Node is, it has one giant drawback: you have to write in JavaScript.

That’s also Node’s advantage. JavaScript is easy to learn and lots of people already know it. But while JavaScript, well, <em>exists</em>, Ruby is lovely.

Ruby has a whole lot in common with Objective-C. Both languages count Smalltalk as an ancestor: both are object-oriented and both use dynamic dispatch. I think you’d like it.

The rest of this post will get you up-and-running with Sinatra. Quickly. In like a minute.

(Yes, I know that many readers of this blog know Ruby and web services far better than I do. This is for the ones that don’t.)

#### Get Sinatra

In Terminal: <code>sudo gem install sinatra</code>

You already have Ruby, since it comes with OS X. <code>gem</code> is Ruby’s package manager. (Think CocoaPods, or think npm if you’re a Node developer.)

You’ll see some messages in Terminal as it downloads and installs Sinatra and its dependencies.

This tutorial will convert some Markdown text to HTML. There’s a gem for that too:

<code>sudo gem install rdiscount</code>

(Markdown? Discount? Got it.)

#### Create the Server

Create a folder on your desktop called CoolWebSite.

Inside that folder create CoolFile.markdown. Its contents should be simple:

<code>\# It Worked!</code><br />
<code>This is a cool web page served by Sinatra</code>

Then, also inside that folder, create CoolApp.rb.

Its contents are your actual Sinatra-based server.

The top two lines are the equivalent of import statements:

<code>require 'sinatra'</code><br />
<code>require 'rdiscount'</code>

Then we have Sinatra’s router, where you match http methods and paths to code. This example has just one route which matches a GET request to /.

The code matching that route does the following:

1. Read the contents of CoolFile.markdown.

2. Turn the Markdown text into HTML.

3. Add the HTML bits to the start and end of the HTML.

<code>get "/" do</code><br />
<code>&nbsp;&nbsp;file = File.open("CoolFile.markdown", 'r')</code><br />
<code>&nbsp;&nbsp;file\_text = file.read</code><br />
<code>&nbsp;&nbsp;file.close</code><br />
<code>&nbsp;&nbsp;markdown\_text = RDiscount.new&#8203;(file\_text).to\_html</code><br />
<code>&nbsp;&nbsp;page\_text = "&lt;html>&lt;head>&lt;title>&#8203;It Worked!&lt;/title>&lt;body>#{markdown_text}&#8203;&lt;/body>&lt;/html>"</code><br />
<code>end</code>

You can see, I hope, that at this point you’re not that far from a blogging engine that reads Markdown files on disk and returns HTML.

#### Run the Server

In Terminal, navigate to your CoolWebSite folder. Type the following:

<code>ruby CoolApp.rb</code>

You’ll see that WEBrick starts up, and you’ll see a message like this:

<code>== Sinatra/1.4.5 has taken the stage on 4567 for development with backup from WEBrick</code>

Now, in your browser, go to <code>http://localhost:4567</code>. You should see the It Worked! page, in glorious HTML. (You can view the page source to confirm.)

That’s it. Now you’re a web developer — and, what’s more, you have an easy-to-learn and lightweight framework plus a language that should feel very familiar. (No square brackets, but I’m confident you can get by without them.)
