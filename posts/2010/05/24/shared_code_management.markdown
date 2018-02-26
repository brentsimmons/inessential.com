@title Shared code management
@pubDate Mon May 24 11:11:26 -0700 2010
@modDate Mon May 24 11:11:26 -0700 2010
We have five Cocoa apps at NewsGator: TapLynx, Social Sites, and three versions of NetNewsWire. They share code.

(You may not have heard of <a href="http://itunes.apple.com/us/app/newsgator-social-sites/id358181841?mt=8">Social Sites</a>. Written by <a href="http://twitter.com/nick_harris">Nick Harris</a>, it’s an iPhone client for our Social Sites enterprise social networking app.)

We’ve just been doing the copy-files thing. Not good. So below I present an (ever-so-slightly edited: took out two words) internal email I just sent about managing the shared code. This is as a sanity check: I think, given our tools, this is the best way to manage this stuff, but I wouldn’t mind hearing that there are other, better ways.

#### The email: “Shared Code Plan”

Here’s the issue: we have a bunch of code that’s shared between two or more apps. We don’t have a way of managing this right now other than just copying files — which is inconvenient at best, and leads to files being not-quite-the-same in different places as bugs are fixed and features added.

Here’s the solution I’m thinking of. If any of this sounds like the wrong way to go, let me know.

- Code shared between two or more apps will all live together in an RSCore repository. (If Apple can keep using NS, we can use RS. I just find the initials more poetic than NG, and that actually, bizarrely, matters to me.) This way the shared code will all be the same for each app.

- Existing and new projects will include the RSCore repository as a Mercurial sub-repository (a sub-folder in the project folder).

- The RSCore repository will have Foundation and UIKit sub-sections. (This way NetNewsWire/Mac can still use the Foundation stuff.)

- A given project will include just what RSCore files it needs. It won’t be presented as a static library, since that makes debugging a pain, and leads to including unnecessary code.

- However, RSCore will have a unit tests project, so we can verify code changes before committing, so we can avoid breaking all our apps at once.

- Category methods on Foundation and UIKit will begin with an rs_ prefix, to avoid namespace collisions.

- New classes in RSCore will be prefixed with RS.

- We’ll be conservative about what we add. *Only* things that are for sure used in more than one app will go in there.

The idea is not to make additional work, but to make less work in the future, to make all this manageable, to increase productivity.

Make sense? Not make sense?
