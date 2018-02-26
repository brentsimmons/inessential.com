@title On Scripting
@pubDate 2015-08-25 11:08:01 -0700
@modDate 2015-08-25 11:08:01 -0700
Graham Lee writes of [The death of scripting](http://www.sicpers.info/2015/08/the-death-of-scripting/) and [The paradox of scripting](http://www.sicpers.info/2015/08/the-paradox-of-scripting/).

>But how can scripting be dead? There’s bash, and powershell, and ruby, and…even Perl is still popular among sysadmins. There’s never been a better time to be a programmer or other IT professional trying to automate a task.

>True, but there’s never been a worse time for someone <em>who doesn’t care about computers</em> to use a computer to automate a task. Apps are in-your-face “experiences” to be “used”, and for the most part can’t be glued together.

There are counter-examples, of course — the apps I work on (Mac versions of OmniFocus and OmniOutliner) are highly scriptable. But the trend toward silos, sandboxing, and highly-controlled experiences is clear.

(First thing I did was look to see if Slack has a scripting dictionary. Of course not. Neither does HipChat. Apps these days.)

If you’re thinking about adding AppleScript support to your app, read these articles from objc.io last year:

[Making Your Mac App’s Data Scriptable](http://www.objc.io/issues/14-mac/scripting-data/)

[Scripting from a Sandbox](http://www.objc.io/issues/14-mac/sandbox-scripting/)

In the first of these, I write:

>When adding AppleScript support — which is also JavaScript support, as of OS X 10.10 — it’s best to start with your app’s data. Scripting isn’t a matter of automating button clicks; it’s about exposing the model layer to people who could use your app in their workflows.

>While that’s usually a small minority of users, they’re power users — the kind of people who recommend apps to friends and family. They blog and tweet about apps, and people listen to them. They can be your app’s biggest evangelists.

>Overall, the best reason to add scripting support is that it’s a matter of professionalism. But it doesn’t hurt that the effort is worth the reward.
