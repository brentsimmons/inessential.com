@title Justin on Auto Layout Debugging
@pubDate 2014-08-27 11:19:54 -0700
@modDate 2014-08-27 11:30:26 -0700
Justin Williams shows how to use <a href="http://carpeaqua.com/2014/08/27/auto-layout-in-ios-8-layoutdebuggingidentifier/">layoutDebuggingIdentifier</a> to help when debugging auto layout in iOS 8.

This sounds *very* useful. It’s private API, so you can use it for debugging only, but that’s totally fine.

I might have taken an alternate approach with the code, though. Instead of `NSSelectorFromString`, the clang pragmas, and <code>performSelector:&#8203;withObject:</code>, I would have done this:

<code>#if DEBUG</code><br />
<code>&nbsp;&nbsp;NSString *identifier = @"Email Label";</code><br />
<code>&nbsp;&nbsp;[self.emailLabel setValue:identifier forKey:&#8203;@"layoutDebuggingIdentifier"];</code><br />
<code>#endif</code>

Not tested, but ought to work.
