@title How to Hang Mail, TextEdit, and Contacts
@pubDate 2015-07-22 15:35:32 -0700
@modDate 2015-07-22 16:20:56 -0700
We often get crash reports where the crash happens outside our code and we can’t reproduce it. (Like every developer, I’d bet.)

While our users often tell us what they were doing when submitting a crash log — thanks! it helps a ton — those steps don’t always have the one key thing we need to be able to reproduce the crash.

But today we got one from a helpful OmniGraffle user: hit the Return key *really, really fast*.

We tried it, and we reproduced the crash. Then reproduced it in other of our apps, then reproduced it in Mail, TextEdit, and Contacts. (And stopped there.)

So I decided to title this post “How to Hang Mail, TextEdit, and Contacts,” because it’s more universal than “How to Crash OmniFocus.” But I’d bet this works on a fair number of apps, Apple’s and not Apple’s.

Before you try it, fair warning: you will have to force-quit TextEdit. When I did this on 10.11, things went weird and I had to reboot.

Here’s what to do:

1. Launch TextEdit.

2. Start a new document.

3. Type a few characters.

4. Save it to your Desktop.

5. Choose File > Export as PDF… and have it export to your Desktop.

6. Choose File > Export as PDF… again — and select the file you just exported to. (As if you’re going to overwrite it.)

7. Hold down the Return key. TextEdit will hang after a few seconds. You’ll have to force-quit it.

8. Open Console. You’ll see something like this:

<code>7/22/15 3:28:25.441 PM TextEdit[866]: \*\*\* Assertion failure in -[NSWindowCentricRemoteView maintainProcess&#8203;NotificationEventMonitor:], /SourceCache/&#8203;ViewBridge/&#8203;ViewBridge-105/&#8203;NSRemoteView.m:1356</code>

Note: to make this work, you may have to have your Keyboard key rate set fairly high in System Preferences > Keyboard. (Mine is at second-fastest.)

Also note: the PDF part is a red herring. It has nothing to do with PDF. That just happened to be a handy example.

Also note: you can do the same thing use Save As… in TextEdit and get a slightly different weird behavior.

[rdar://21949944](rdar://21949944)

#### Update 4:20 pm

It may not hang on 10.11 b4. You might see some display strangenesses — like black rectangles where a sheet used to be. And you may see notes in Console from com.apple.appkit.xpc.&#8203;openAndSavePanelService.
