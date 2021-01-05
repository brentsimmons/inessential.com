@title Bogus Code Signing Crash
@pubDate 2021-01-04 23:02:37 -0800
@modDate 2021-01-04 23:02:37 -0800
For a few people, NetNewsWire for Mac crashes on startup — and the crash log erroneously blames an invalid code signature.

If it were truly invalid, the app wouldn’t launch for anybody. But it launches fine for almost everybody.

This started with macOS 10.15.4 and continues in macOS 11. We’ve posted [more details on our issue tracker](https://github.com/Ranchero-Software/NetNewsWire/issues/2704) at GitHub.

Does anybody have any ideas for how to work around this?
