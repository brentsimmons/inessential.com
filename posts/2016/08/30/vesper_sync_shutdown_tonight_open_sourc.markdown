@title Vesper Sync Shutdown Tonight, Open Source Plans
@pubDate 2016-08-30 09:44:52 -0700
@modDate 2016-08-30 09:44:52 -0700
#### Sync Shutdown Tonight

We will turn off Vesper’s syncing service tonight at 8pm Pacific. Though syncing will stop working, other things won’t.

* Data is stored on your device. The app will continue to work even without syncing. You can continue to use the app.

* You can still export your data. As many times as you want. The Export feature works with the data on your device — it has nothing to do with syncing.

* We plan to remove the app from the App Store Sept. 15, but you can continue to use the app even after that. The Export feature will continue to work after that.

I think that covers everything, but I may update this post if we find people asking questions that haven’t been covered by the above.

#### Open Source Plans

We plan to do all of the below by the end of 2016, but we can’t make promises. (Life may intervene.)

Q Branch’s existing open source code — <a href="https://github.com/quartermaster/DB5">DB5</a> and <a href="https://github.com/quartermaster/QSKit">QSKit</a> — will be moved to my personal GitHub account. I will continue to maintain DB5 (I continue to use it). QSKit will not be maintained, but will be made available as historical artifact.

We will make Vesper for iOS, Vesper for Mac, and Vesper’s JavaScript sync service open source on my personal GitHub account. This code will also be provided as historical artifacts: they’re not intended as active projects. They’re also not intended as examples of how to write apps these days.

The licenses will be public domain or something roughly as non-restrictive. However: the name Vesper and the app icon remain the property of me, Dave, and John. If you build anything based on this code, you must pick a different name and different app icon.

Other notes:

* Before being posted, Vesper for iOS will be revised so that it uses the default system font, since we can’t ship Ideal Sans as part of this. I’ll probably also adopt Dynamic Type as part of this work. (Since it’s the right thing to do.)

* Vesper for Mac is most definitely incomplete.

* The syncing backend runs on Azure Mobile Services, which is Node.js plus a bunch of goodies. It’s not something you can just upload and run anywhere — but the code might still be useful to look at.

* In Vesper there is good code and bad code and so-so code. Part of the fun of this will be me writing blog posts ripping apart the bad code. You have no idea how much I’m looking forward to that. :)
