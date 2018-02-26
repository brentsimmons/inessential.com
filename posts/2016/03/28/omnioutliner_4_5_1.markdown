@title OmniOutliner 4.5.1
@pubDate 2016-03-28 12:13:14 -0700
@modDate 2016-03-28 12:14:14 -0700
The <a href="https://www.omnigroup.com/omnioutliner">latest OmniOutliner for Mac</a> is up. (It will be in the app store once it passes review. This week is my guess.)

<a href="https://www.omnigroup.com/releasenotes/omnioutliner-mac">Changes include</a> some printing bug fixes — and also a fix for a cosmetic bug that was driving me crazy: in the sidebar, when you collapse or expand the Styles, the Contents outline will now stay in place. (Previously it was changing position then changing back. Animatedly.)

The fix, by the way, was just to switch to a flipped NSView, so that 0,0 is at the upper left rather than bottom left. Given that we’re using auto layout, I didn’t expect the flipped-ness of a view to matter, but it does. (I should have known better.)
