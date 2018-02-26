@title Evergreen Diary #5: Send to MarsEdit
@pubDate 2018-01-15 14:26:26 -0800
@modDate 2018-01-15 14:26:26 -0800
The [latest build of Evergreen](https://ranchero.com/evergreen/), fresh from the lab, now adds [MarsEdit](https://red-sweater.com/marsedit/) to the sharing menu in the toolbar.

When you choose the command, it sends the current article to MarsEdit — which opens it in a new window, and then you can edit and add your own commentary before posting to your blog.

<p style="text-align:center">* * *</p>

See [SendToBlogEditorApp.m](https://github.com/brentsimmons/Evergreen/blob/master/Frameworks/RSCore/RSCore/AppKit/SendToBlogEditorApp.m) for the code that packages up the article and sends an Apple event.

The code is *not* MarsEdit-specific — other apps in the past have supported this same Apple event, though I don’t know if any other current apps do. If I find some, I’ll add them to the sharing menu alongside MarsEdit.

<p style="text-align:center">* * *</p>

The Apple event code is written in Objective-C, even though I almost always write new code in Swift. But, with Apple events code, Objective-C is easier.

It’s easy to call from Swift: see [SendToMarsEditCommand.swift](https://github.com/brentsimmons/Evergreen/blob/master/Commands/SendToMarsEditCommand.swift).

(Reminder: this is all MIT-licensed. You can use this code.)
