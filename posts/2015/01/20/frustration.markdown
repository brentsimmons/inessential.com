@title Frustration
@pubDate 2015-01-20 10:20:23 -0800
@modDate 2015-01-20 10:20:23 -0800
When Mac and iOS developers get together, we complain about Apple bugs — which will *always* be true, whether or not the number and severity of bugs is actually high.

If we can’t grumble, we can’t be happy. So we grumble.

If you and I were sitting at a table, here’s the story I’d tell you:

WebView has a bug where scrolling is messed-up in some cases where you have a div that needs to stay anchored to one side of the window. (Think of a header that doesn’t move while the rest of the content moves.)

But the new replacement for WebView — WKWebView — doesn’t have this bug. Which is great. Let’s adopt the new thing! I’m all in. Love new things.

So I did, and it’s great. So happy. Until I noticed the console message:

<code>Could not create a sandbox extension for '/'</code>

I did some research, and I learned that WKWebView won’t show local content — that is, files that are loaded from the app’s bundle. Files from the app bundle ought to be a-okay, ought not be a sandbox violation, but apparently they are.

So while this works fine in my development build, research tells me it won’t work for the release build.

Do I need to write and embed a small web server in the app just to make this work? (Na ga da.) Instead, let’s just put the files on the web, because *of course* the web is safer than files distributed in the app bundle. (That right there was sarcasm.) It means the feature won’t work when off-line, but there are mitigating factors that make that mostly okay. Okay enough.

So: great. Problem solved!

*Until*, that is, I went to wire up the Find command. WebView has a <code>searchFor:&#8203;direction:&#8203;caseSensitive:&#8203;wrap:</code>. It’s not as great as the Find feature in Safari, but it’s okay for what I’m trying to do. (At least for now.)

WKWebView has nothing even similar. So now I don’t know what to do.

In an ideal world, WKWebView would work with files from the app bundle, and, as a replacement for WebView, it would have the same functionality as WebView (a searchFor or equivalent method). Anything else means running as fast as I can while I slip backwards.
