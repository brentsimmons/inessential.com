@title UITableViewCell Is Not a Controller
@pubDate Mon Dec 31 15:53:58 -0800 2012
@modDate Mon Dec 31 16:00:30 -0800 2012
In a <a href="http://inessential.com/2012/12/31/coders_in_the_hands_of_an_angry_god">previous post</a> I wrote that passing model objects to a UITableViewCell subclass is a bad practice.

Some people asked me why, so I’ll explain.

#### What I mean by model object

By model object I don’t mean NSStrings, numbers, and so on. I mean the thing that a table row represents, which is typically an object with a bunch of properties.

If it’s a song, for instance, it would have properties such as artist, title, duration, and the number of times played.

I’m not against passing those values to the cell: I’m against passing the song object to the cell.

#### It goes against MVC

If a UITableViewCell knows about a model object, then the UITableViewCell is responsible for taking data from the model object and displaying it. But that’s not typically the way we work. Cocoa is an MVC-based system, which means that controllers come between models and views. A UITableViewCell is a view, not a controller.

In the case of table views, there will be an object, typically a UIViewController or UITableViewController, that implements (usually both) UITableViewDataSource and UITableViewDelegate protocols. That object is the controller, and it has the job of coming between the model and the UITableViewCell.

#### Aren’t rules meant to be broken?

MVC is a useful design pattern — it’s not a straightjacket we’ve all agreed to wear. There are times when an expedient short-circuit is easier, more clear, and more maintainable.

Right?

Here’s President Obama quoted in <a href="http://www.vanityfair.com/politics/2012/10/michael-lewis-profile-barack-obama">Obama’s Way</a> by Michael Lewis:

>“You’ll see I wear only gray or blue suits,” he said. “I’m trying to pare down decisions. I don’t want to make decisions about what I’m eating or wearing. Because I have too many other decisions to make.”

As a programmer you make decisions all day (and maybe all night) long. When a choice between MVC and anything else comes up, choose MVC. Save yourself from decision fatigue — because you want to be at your best for all the *hard* choices.

When I was a less-experienced programmer I would have disagreed with the above. I would have replied that there’s no excuse for not using your brain.

But over the years I’ve learned that one of the keys to working intelligently is recognizing when you’ve encountered a settled matter, and being wise enough to avoid wasting any decision energy when those come up.

Still, though — yes, there may be times when doing something other than strict MVC is the best thing. Mmmmmmaybe.

But here are some of the issues you could run into if you do think you can get away with not-MVC.

#### Asynchronous images

Imagine the common case where a UITableViewCell needs an image, and the image is loaded asynchronously from the web. It comes from the web and is probably cached on disk or in a database and also cached in-memory.

Spot the problem with this code:

<code>[self.imageFetcher fetchImage:someImageID completionBlock:&#94;(UIImage *fetchedImage) {<br />
&nbsp;&nbsp;self.imageView.image = fetchedImage;<br />
}];</code>

Since <code>fetchImage:completionBlock:</code> is asynchronous, you can’t know when the block will be called. The fetched image may no longer be the appropriate image to show in the view — the cell may have been recycled.

So you could add something that checks to see if that’s still the correct image. But you’re starting to stand on your head at that point. And you’ll also note that possibly several UITableViewCells have asked for the same image to get fetched, possibly causing a performance hit.

It’s much better to do this work in the controller class — it can ask for each needed image exactly once, and it can create an in-memory cache that disappears when the controller is dealloced.

There are other ways you might design this — but I don’t know of a better way to handle it than in the view controller.

#### UITableViewCell re-use

You may be convinced that you’ll never, ever need to use your UITableViewCell with anything other than that particular model object.

But consider some cases where you might:

1. In a UI walk-through or help system you want to show a UITableViewCell with example data. (Okay, I know — don’t do UI walk-throughs. Unless you’re getting paid to do it.)

2. In the theming setting screen, you may want a UITableViewCell with example data. (Okay, you tell me you’ll never do theming. But what if Loren Brichter releases an <a href="https://itunes.apple.com/us/app/letterpress-word-game/id526619424?mt=8">app with theming</a>, and now you think it’s cool and you want to do it too?)

3. You’re writing something like a Twitter app, and you want to display the tweet-being-uploaded in the table — but your model objects are NSManagedObjects, and the tweet-being-uploaded can’t be turned into an NSManagedObject until you get the response back from the server with its uniqueID and other server-generated properties.

4. You’re writing something like iTunes, and you go from having local-songs-only to local songs and songs-in-the-cloud — and they’re not the same model object. They may be similar, of course, but they’re not the same. Do you create a bunch of logic in the UITableViewCell to handle the differences?

One possibility leaps to mind: use protocols. Have the UITableViewCell take objects that conform to that protocol. That would solve all of the above.

Protocols are awesome. But as soon as you make that protocol you also have to make at least one other object which implements that protocol. At that point you are multiplying entities — and you’re standing on your head when you could have just had the view controller do its job as a controller.

#### Updating via the web

Last scenario. You’re writing an app where the data in the app can change outside of your app — it pulls data from the web, and your model objects update. (Maybe even just because the app syncs with other clients.)

How do the UITableViewCells get updated?

You could have each cell do key-value observing — but then you’re setting up and tearing these down frequently, at a cost to performance. (And you’ll probably have to implement <code>prepareForReuse</code>, which I consider a code smell.)

Or you could have it register for more-generic NSNotifications, but then each cell will be checking to see if the notification applies or not (also smelly and inefficient).

The best way to handle this is obvious: the view controller should get the change notifications and update the cells that need updating.

#### What I do

Enough scenarios. Now for practical stuff.

I use the same idea for every table view.

1. The view controller implements <code>tableView:cellForRowAtIndexPath:</code>, which calls a method like <code>updateCell:atIndexPath:</code>.

2. The view controller has registered for various types of notifications, and when a notification arrives it looks at the visible cells and determines which, if any, need updating. Then it calls <code>updateCell:atIndexPath:</code> for each cell that needs it.

3. The <code>updateCell:atIndexPath:</code> method is where model object properties get passed to the cell, often transformed.

The key here is, obviously, the <code>updateCell:atIndexPath:</code> method. By having a single method that passes values to the cell, I have one place that translates a model object to the values the cell needs. And it can get called both from <code>tableView:cellForRowAtIndexPath:</code> and from any notification handler.

Another key is to use UITableView methods <code>cellForRowAtIndexPath:</code>, <code>visibleCells</code>, and <code>indexPathsForVisibleRows</code> so you can translate between model objects and visible rows (and vice versa).

If you haven’t done it before you’ll have to figure it out. But it’s pretty simple — and, once written, you’ll find it easy to use every time after that.

#### Well

Still, there are other ways you could do this. You could keep passing model objects to UITableViewCells and find good designs that deal with everything I’ve mentioned above.

But why? MVC works. We already know it works.
