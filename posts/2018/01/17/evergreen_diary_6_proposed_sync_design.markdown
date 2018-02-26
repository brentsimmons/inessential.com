@title Evergreen Diary #6: Proposed Sync Design
@pubDate 2018-01-17 21:02:45 -0800
@modDate 2018-01-18 13:15:10 -0800
Most of the time, a user will do a thing — mark some articles as read, for instance — and then Evergreen will tell the server ([Feedbin](https://feedbin.com/), [Feedly](https://feedly.com/), etc.) right away. That’s good and easy.

The hard part is this: what happens when the server is not reachable for some reason?

Continuing the example: Evergreen could, in the case of the unreachable server, refuse to mark those articles as read.

It could insist that syncing works only when the server is reachable — which is not *that* weird, especially given that it can’t pull new data from the server unless it’s reachable.

But it’s weird enough. Consider that selecting an article marks it as read. This policy would make it impossible to even *just read* what you’ve already downloaded.

#### Offline Syncing

It’s clear that syncing requires some sort of offline ability.

Rather than set a policy for each possible user action (marking articles read, deleting a feed, etc.), I want to set a single policy and single structure for handling these actions.

(Note: there will be some things that do actually require a reachable server: downloading new articles and adding a feed come to mind. This design refers to actions where it would be okay to defer notifying the server.)

#### Proposed Policy

When the user performs a syncable and deferrable action, that action and the relevant parameters will be remembered.

Evergreen will attempt to notify the server periodically. Once it succeeds, it will forget that action and its parameters.

(Update 18 Jan: 2018: the original version of this design had a time limit, which has been removed. The concern was that this offline queue would grow unbounded — but it can’t, since if you can’t reach the server you can’t download new articles, which means the queue is limited to your current local data set.)

#### Proposed Implementation

When the user performs a deferrable action, the app tries immediately to notify the server.

If this first attempt fails, then the action is recorded in a SQLite database with a timestamp and with the parameters it needs to be able to make that call again later. Those parameters will be minimal — article IDs instead of entire Article objects, for instance.

The app will periodically attempt to empty this database: starting with the oldest action, it will notify the server of each. On success, a given action is removed from the database.

#### Undo

Evergreen supports undo as much as possible. For instance, if you mark a number of articles as read, you can undo it.

In this case, Evergreen will notify the server of the mark-read action, and then, upon undo, notify the server of a mark-*unread* action, thereby undoing the effect of the first action.

In the case where the mark-read action is in the offline action queue, that will be found and deleted, and there will be no queued action to reverse the effect.

#### Non-Deferrable Actions

Actions that require an immediate response from a reachable server include actions such as adding a feed. In the case where a user attempts one of these and the server can’t be reached, an error sheet will explain the problem. Such actions will not be queued.

There will not, however, be an error sheet for performing a refresh when the server is unreachable. Instead, in that case, a warning icon is placed next to it in the sidebar, a la Mail and similar apps. Clicking the icon will attempt a connection to the server, and an error sheet explaining the problem will appear if the server still can’t be reached.

#### Other Notes

Evergreen works like Mail and similar apps in that it has a set of accounts for services such as Feedbin, Feedly, and others, along with an On My Mac account that is not synced.

Each account has its own section in the main window’s source list; each account has its own set of folders and feeds.

Accounts will be added to Evergreen in Preferences, in an Accounts pane.

The policies of these accounts will be respected. For example, if the On My Mac account automatically marks articles as read after n days, it’s possible that some service does this after some other number of days, or never does that at all, and Evergreen won’t override those policies for that service.

Another example: the On My Mac account doesn’t support folders-within-folders — but if a feed service does support that, then the app will support it too, for that service.

(Current plan: Evergreen 1.0 will ship with Feedbin support, and Evergreen 2.0 will add support for more services.)

Let me know if any of the above sounds weird or if I missed anything. (There is contact info at the bottom of [Evergreen’s main page](https://ranchero.com/evergreen/).)
