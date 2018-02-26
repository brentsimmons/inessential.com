@title One Way to Avoid Singletons
@pubDate 2014-03-13 12:50:18 -0700
@modDate 2014-03-13 13:16:51 -0700
I don’t particularly like global objects with a single instance when they get attached to the app delegate or are made available via a sharedInstance class method.

I do it, sure — sometimes it’s the least-bad option. But I try to keep it to a minimum.

In my code it’s a frequent issue with caches. Real-life example: Vesper’s timeline has multiple row heights, and so there’s a VSRowHeightCache so those row heights don’t have to be recalculated.

But I *don’t* want VSRowHeightCache hanging off the app delegate. Rather, what I want is for each timeline view controller to get its own cache via `[VSRowHeightCache new]`.

But I *also* want all VSRowHeightCache instances to use the same data, *and* I want the cache to be able to watch for notifications that trigger removal from the cache.

Here’s how I make that work.

#### Static Cache

Inside VSRowHeightCache.m, there’s a static rowHeightCache that all instances use.

<code>static NSMutableDictionary *rowHeightCache = nil;</code>

(The dictionary is created inside `+initialize`, inside a `dispatch_once` block.)

I don’t particularly like static variables, but at least it’s limited to the file it’s in. I consider this better than attaching a VSRowHeightCache to the app delegate.

There are also some static C functions that get, set, and delete items from the cache. Those wouldn’t have to be C functions, but I like using C because it signifies that they’re the private, low-level, shared-across-instances functions for manipulating the cache. Only the C functions are allowed to access the rowHeightCache dictionary directly.

Functions look like this:

<code>static void cacheHeightForUniqueID(int64_t uniqueID, CGFloat height) {</code><br />
<code>&nbsp;&nbsp;rowHeightCache[@(uniqueID)] = @(height);</code><br />
<code>}</code><br />

So: problem halfway solved. Multiple VSRowHeightCache instances share the same data.

#### Notifications

The cache also needs to know when it should delete items. It watches for insert and update notifications from the model layer. When a note changes, its row height should be removed from the cache so it can be recalculated later.

It also watches for changes to typography settings, and removes all cached heights when typography settings change.

But having separate instances of VSRowHeightCache register for notifications means it could be doing extra work. And of course there are times when there’s no VSRowHeightCache instance, and then the un-caching wouldn’t happen, which would be bad.

This is easily solved by having the class itself register for notifications.

Inside `+initialize`, inside a `dispatch_once` block, the VSRowHeightCache registers for insert and update notifications and typography-settings-did-change notifications.

It then has class methods that handle the notifications, that then call the C functions that directly manipulate the cache.

#### Problem solved

I can instantiate as many VSRowHeightCaches as I want to, and the cache will continue to work as expected: all instances will share data. And the underlying cache dictionary will be maintained even when there are no instances.

All this goes on inside the file. The public API is super-simple:

<code>- (CGFloat)heightForTimelineNote:&#8203;(VSTimelineNote \*)timelineNote;</code><br />
<code>- (void)cacheHeight:(CGFloat)height timelineNote:&#8203;(VSTimelineNote \*)note;</code>
