@title Sign All the Things
@pubDate 2014-08-05 12:15:27 -0700
@modDate 2014-08-05 12:16:23 -0700
Daniel Jalkut writes up <a href="http://indiestack.com/2014/08/take-this-code-and-sign-it/">how he code-signs his Mac app</a>. It’s a good solution — that I hope I never have to do.

I haven’t been in this position yet — I haven’t had a Mac app distributed outside the Mac App Store (or a Mac app at all) in a few years.

But I bet my solution will be to not use embedded frameworks.

It’s still possible to use shared code, after all. Even sub-repositories. It’s just that the files are included in the app target, rather than built as frameworks.

It may be less elegant in some ways, but it’s the way I’ve been doing things on iOS for a while now, and it’s working fine for me. It has the added benefit of allowing me to pick and choose what I need from a set of shared code.

Example: <a href="https://github.com/quartermaster/QSKit">Q Branch Standard Kit</a> includes some XML parsing stuff, but Vesper doesn’t need it. If we had a Q.framework that included everything, then Vesper would include code it doesn’t actually need.
