@title How We Work Together
@pubDate Fri Jun 07 11:09:56 -0700 2013
@modDate Fri Jun 07 17:22:06 -0700 2013
Since I’m always interested in hearing what other teams use to work together and ship their software, I figure I should list what we use to work together on <a href="http://vesperapp.co/">Vesper</a>.

#### Mercurial

To swim with the current these days is to use git. But I like <a href="http://mercurial.selenic.com/">Mercurial</a> better — and I think Mercurial is to Macintosh as git is to Windows. That’s probably not fair or rational, but it doesn’t really matter, since both git and Mercurial are excellent systems.

Along with Mercurial we use <a href="https://bitbucket.org/">Bitbucket</a>. I rarely had to log in to the site — which is as it should be. It just worked.

All of us use Mercurial on the command line.

#### Glassboard

Almost all of our company communication is via <a href="http://glassboard.com/">Glassboard</a>. We’ve sent just a few emails and a few more text messages — but mostly it’s been Glassboard.

(This is the second app I’ve shipped with the aide of Glassboard. The first was Glassboard itself.)

In addition to our company board, we have a board that includes <a href="http://www.takingnotes.co/">Doug Russell</a> and <a href="http://www.neglectedpotential.com/">Nick Arnott</a>, our accessibility and QA experts, and we have a board for beta testers.

In the past, before Glassboard, we would have used a discussion list because it’s valuable when testers are able to discuss things with us and each other. It becomes collaborative, and it makes for better software.

My first experience with this model goes back to my days at UserLand Software in the ’90s when we had a testers mailing list for Frontier. It was so productive, and so much fun, that I’ve used this same model for all of my subsequent apps.

#### Lighthouse

<a href="http://lighthouseapp.com/">Lighthouse</a> bills itself as “beautifully simple issue tracking,” and to its credit I’m not sure what else there is to say. It’s a bug tracker. It looks nice. It’s easy to use. It works well.

We made heavy use of the milestones feature. We tend to tag tickets. We don’t order tickets by priority. (My internal algorithm defeats priorities. When there isn’t a clear choice, I pick based on how long it is till dinner, whether or not I’m tired, what I just completed, and what mood I’m in.)

In the last few weeks of the project, I measured progress by calculating how many tickets we’d have to close per day. If that number kept going up, then hitting our ship date was at risk. (We hit our date.) (After revising our early naive schedule.)

#### HockeyApp

We use <a href="http://hockeyapp.net/">HockeyApp</a> to distribute builds to testers. My favorite HockeyApp feature: symbolicated crash logs. My second-favorite feature: email notifications when there’s a crash.

In the past I’ve used <a href="https://testflightapp.com/">TestFlight</a>, which I also like very much. Both are an <em>incredible</em> improvement over the old days of passing around .ipa files and provisioning profiles.
