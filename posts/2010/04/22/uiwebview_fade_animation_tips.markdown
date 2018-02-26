@title UIWebView fade animation tips
@pubDate Thu Apr 22 12:09:11 -0700 2010
@modDate Thu Apr 22 13:38:37 -0700 2010
Say you want to fade between one UIWebView and another (as NetNewsWire/iPad does when switching articles, or going from article to web page or back). The first one fades to 0.0 alpha and then goes away. Two tips:

1. The first one — the one going away — should be on top. (It should fade away, revealing the webview beneath.)

2. It will look weird unless you set the background color of the first one (going-away-one) to UIColor clearColor.
