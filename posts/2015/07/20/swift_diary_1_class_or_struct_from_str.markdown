@title Swift Diary #1: Class or Struct from String
@pubDate 2015-07-20 09:39:20 -0700
@modDate 2015-07-20 10:08:08 -0700
Like Mike Ash and his <a href="https://mikeash.com/pyblog/">Friday Q&A blog posts</a>, I take requests from readers. Unlike Mike Ash, all I have is questions.

This one comes from my co-worker <a href="https://twitter.com/jimcorreia">Jim Correia</a>, and is related to a question I posted on Twitter last night about instantiating an object whose class is known at runtime rather than compile time.

For reference, here’s the <a href="https://gist.github.com/brentsimmons/2080595ac8a6f41711af">answer to last night’s question</a>.

Jim takes this one step further: what if all you have is the class name as a string?

This isn’t an academic question — it’s something app developers do. For example, do a Show Package Contents on any Omni app and look inside Info.plist — you will likely find class names in the plist. (Example: see OFControllerClass in OmniFocus’s plist. Also look inside the OIInspectors array.)

This is a useful pattern when you have a general framework of some kind and you want to configure it for a specific app. The framework doesn’t know which specific classes to use, so you tell it.

And then, in the code, at some point it comes down to doing an `NSClassFromString(s)` to get a class, and then instantiating an object.

I want to do the same thing in Swift, but with additional criteria:

* I don’t want to have to mark the class an Objective-C class. I want to use pure Swift.

* I want to be able to use structs interchangeably with classes. Whether the thing is a class or a struct is a detail that’s private to the class or struct, and not something the general framework needs to know.

I realize that this may seem marvelously unsafe to some people. But, in practice, it’s not. And it’s super-common. (And it’s not terribly different from working with Interface Builder, where you configure by typing in class names.)

I’ll update this post with the answer. (I assume there is one.)

<p style="text-align:center">* * *</p>

<b>Update 10:05 am:</b> <a href="https://twitter.com/jckarter/status/623174519939674112">@jckarter writes</a>:

>Possible, but not implemented yet.
