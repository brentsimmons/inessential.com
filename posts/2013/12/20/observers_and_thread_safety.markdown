@title Observers and Thread Safety
@pubDate 2013-12-20 13:23:10 -0800
@modDate 2013-12-20 13:29:15 -0800
A friend of mine at Xcoders told me about threading issues with NSNotificationCenter and KVO. In my own code I always [post notifications on the main thread](https://github.com/quartermaster/QSKit/blob/master/Classes/Foundation/NSNotificationCenter%2BQSKit.h) and do any KVO-triggering on the main thread (for precisely the reasons he spells out) — so it’s not an issue I’ve run into. But it’s something you should be aware of.

My friend elaborated via email. Below is his email (edited for typography and typos only):

<p style="text-align:center">* * *</p>

In most ways that matter NSNotificationCenter is thread safe. You can add/remove observers from any thread and you can post notifications from any thread. You’re on the hook for the thread safety of your observer/selector or block handler, but that’s a pretty reasonable way for the API to work.

Here’s a pretty normal pattern for using notification center:

<code>- (instancetype)init</code><br />
<code>{</code><br />
<code>&nbsp;&nbsp;self = [super init];</code><br />
<code>&nbsp;&nbsp;if (self)</code><br />
<code>&nbsp;&nbsp;{</code><br />
<code>&nbsp;&nbsp;&nbsp;&nbsp;[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(prompt:) name:@"PromptUserToRateApp" object:];</code><br />
<code>&nbsp;&nbsp;}</code><br />
<code>&nbsp;&nbsp;return self;</code><br />
<code>}</code>

<code>- (void)prompt:(NSNotification *)note</code><br />
<code>{</code><br />
<code>&nbsp;&nbsp;// Do something async</code><br />
<code>}</code>

<code>- (void)dealloc</code><br />
<code>{</code><br />
<code>&nbsp;&nbsp;[[NSNotificationCenter defaultCenter] removeObserver:self];</code><br />
<code>}</code>

and then somewhere else in your code:

<code>[[NSNotificationCenter defaultCenter] postNotificationName:<br />@"PromptUserToRateApp" object:nil];</code>

This is a perfectly safe thing to do if all those things are happening on the same thread OR if you can guarantee that dealloc will run on the same thread as your -postNotification: calls (or doesn’t run like in the case of singletons.)

Where it gets hinky is when -postNotification: can run on any thread (and therefore so can dealloc because -postNotification: will retain/autorelease it before running.)

#### Here’s the bug:

Thread 1 calls release taking retainCount down to 0 meaning the object will be dealloced. Your object is dead, is just doesn’t know it yet and there’s no coming back.

Thread 2 comes in and posts a notification, for this case let’s assume synchronously since that’s the common case with the observer/selector API. Observer is retained before calling because notification center keeps an unretained reference to observer and wants to make sure the object is alive. Thing is, you can call retain on an object that’s already in dealloc and that doesn’t stop dealloc from finishing and turning that object into a zombie. So now thread 2 is calling into -prompt: and self is in the middle of becoming garbage so nothing you can do in -prompt: will be safe.

Thread 1 gets into dealloc, the observer gets removed and self becomes garbage rendering anything async you did in -prompt: very dangerous. (Doesn’t even have to be async, but that’s the most pronounced case for this problem.)

This same problem manifests with KVO in a nearly identical way and also with notification centers block based API, although in that case it’s actually the internal __NSObserver object that can end up as the bad object being referenced and there’s the added fact that the observer gets retained and then the block gets scheduled asynchronously so if the scheduling hits while in dealloc, the block will almost certainly run after dealloc has finished.

#### So what do I do?

There are a few options:

<strong>Serialization</strong> - Run everything on one thread, not exactly elegant, but it does take a lot of the guess work out. This is actually pretty normal if you’re handling notifications in a view controller posted by system API that promises to run on the main thread. Although, this can fall down pretty easily though because making sure dealloc runs on a specific thread when blocks and autorelease pools exist can be incredibly hard.

<strong>Block based API</strong> - In practice it’s much harder to hit this issue with the block based API due to the lifetime of the observer object it gives back, but it’s definitely not impossible with some well placed autorelease pools and the block based API is also a snake pit of subtle bugs for many developers.

<strong>Objects with safe lifetimes</strong> - This issue doesn’t present at all if your target is for example a singleton. Not that I’m suggesting you use more singletons, but if you already have a data controller singleton, it’s a perfectly safe target for threaded notifications.

<strong>Don’t use notification center</strong> - Ya know what’s great? Weak delegates. The self zeroing weak references in ARC are great and one behavior they offer that’s incredibly useful is that they return nil once an object is going to be dealloced, even before dealloc runs.

This code is totally thread safe:

<code>id&lt;MyProtocol> delegate = self.delegate;</code><br />
<code>if ([delegate respondsToSelector:<br />&nbsp;&nbsp;@selector(prompt:)])</code><br />
<code>{</code><br />
<code>&nbsp;&nbsp;[delegate prompt:nil];</code><br />
<code>}</code>

It’s not strictly required that you use the local ivar, but it’s a good idea since it guarantees that if you get a value back, it will be retained (under ARC) into the local strong variable and live at least through the scope of calling the delegate method.

I’ve always liked delegates. These days I like them even more.

P.S. For people grumbling about how notification center should use weak refs internally, there’s some merit to that, but the unexpected side effects of when weak refs zero can lead to some oddball bugs like if there are multiple observers that are the same except they are registered with different objects (for filtering purposes) and then they all go to zero and you have to decide which one to remove when -removeObserver: is called. It’s not as straightforward as it might seem.
