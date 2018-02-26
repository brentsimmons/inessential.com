@title Vesper Sync Diary #18 - Where the API Logic Lives
@pubDate 2014-07-02 11:02:20 -0700
@modDate 2014-07-02 13:01:28 -0700
(This isn’t really a diary anymore — I’m just explaining things already written. But I might as well make this part of the same group of posts.)

On Twitter, <a href="https://twitter.com/leemorgan/status/484105795127099394">Lee Morgan asked me</a>:

>…suggestion for where API logic lives? in Model? ViewController? an API class?

Here’s where everything goes:

The VSAccount object is the top-level object for syncing. It has username and password; it has methods for creating an account, logging in and out, and syncing. The VSAccount object exists whether or not the user has an actual account and is logged-in. It also knows about the app’s data model.

The VSAccount object knows about the VSAPICaller object (it’s the only thing that knows about it). The VSAPICaller object has methods for each of the different calls that go to the server. It has an NSURLSession and a queue. VSAPICaller doesn’t know about the account or any of its state — its methods take parameters sent from VSAccount. It also doesn’t know about the app’s data model (it gets JSON objects from VSAccount).

The VSAPICaller object creates VSAPICall objects, which are conceptually like NSOperation subclasses (though they’re not). A VSAPICall object creates the NSURLSessionDataTask and handles things like expired authentication tokens.

There are some delegates and blocks in all this. Most notably, VSAPICall calls back to VSAPICaller, and then VSAPICaller calls back to VSAccount, when an API call completes. The callbacks all take a VSAPIResult object, which includes properties such as the request, response, error, statusCode, parsed JSON object, raw response data, and so on. This way, when VSAccount gets a response, it can look at everything: there’s nothing hidden from it.

Syncing is triggered by a number of different things. For things like the app launching and coming to the front, for an account being created, for notes being edited, there are notification observers in VSAccount which call the sync method.

Other callers can directly tell VSAccount to sync, but none do. (Since it’s not needed, I should remove that method from the .h file.)

Calls to the sync method are coalesced: the method can get called a bunch of times in a row, and it will run just once after a delay of two seconds after the last call.

When data is returned from the server, VSAccount uses two other objects, VSSyncNoteMerger and VSSyncTagMerger, to merge server data and local data. Those two objects understand the JSON the server returns and they know about the data model, and they create and update local objects as needed.

The model objects don’t know anything about API calls or syncing. (They can turn themselves into JSON and back again, but I’m working on changing that to use a separate intermediate object instead. I have good reasons for this.)

Model objects *do* however have to differentiate between user changes and syncing changes.

Consider what happens when a user archives a note: the archived flag is set to YES, the archivedModificationDate is set to the current date, and the note’s local modification date is set to the current date. (The query that gets notes to send to the server looks at the local modification date.)

But if the sync system marks a note as archived, it should set the archived flag to YES and it should make archivedModificationDate the same as what the server says it is. It should *not* change the local modification date, since that would just cause the sync system to send the note to the server again when it doesn’t need to.

This is a pain, because it means that the model objects have to have methods like <code>userDidMarkAsArchived:</code> which do the right thing. (The sync system just accesses properties directly.) If there were a better alternative, I’d use it, but I don’t know what that would be.

#### What I Like About All This

I like my model objects to be dumb containers for properties. They are, after all, just an objectified version of a database row, and I like to keep them that way, as much as possible.

I also like to keep my view controllers free of any syncing or API logic. Instead, they make changes to the model and react to changes — they don’t need to know that the changes came from a sync versus a user change.

The only view controllers that need to know about the server are the view controllers in the UI for creating an account, signing in, and so on. Those view controllers may need to display an error or dismiss a view controller (etc.) based on the result of an API call.

But, importantly, and worth stressing: those view controllers don’t actually know how to make the call to the server — they just know how to call <code>createAccount:password:callback:</code> and similar VSAccount methods.

