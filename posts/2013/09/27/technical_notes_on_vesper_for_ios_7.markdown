@title Technical Notes on Vesper for iOS 7
@pubDate Fri Sep 27 16:50:21 -0700 2013
@modDate Fri Sep 27 17:32:55 -0700 2013
(<a href="http://vesperapp.co/appstore">Vesper for iOS 7</a> is on the App Store.)

#### TextKit

You remember in Lord of the Rings when Gollum finally gets the ring and he’s holding it up and dancing around? That’s me and TextKit.

So happy together.

Vesper’s detail view — with separate fonts for title and text — was *barely* possible in iOS 6. Dealing with changes in formatting meant replacing the `attributedText` and restoring the selection.

But TextKit changed that. You can change the formatting attributes of part or all of the `attributedText` without replacing the `attributedText`. *Way* better.

There’s a bunch more to TextKit — but just that one thing was huge for Vesper.

I didn’t, by the way, end up using TextKit for the notes list. We already had working code that used Core Text, and there was no reason to change that code, so we didn’t.

While I love TextKit, I didn’t love `UITextView` that much. There are new bugs, and we couldn’t work around all of them. But `UITextView` in iOS 7 is really a 1.0 release, and so I forgive it. (I need to file some Radars.)

#### 64-bit Support

It took just a few minutes. I bet that’s true for most apps, though games might be an exception. (I don’t know much about games; I could be wrong.)

Since I’d been through this same transition on the Mac, I was already careful to always use NSInteger, CGFloat, and friends.

The compiler caught all the places I needed to make changes. (I use [Hosey-level warnings](http://boredzo.org/blog/archives/2009-11-07/warnings).)

There were a bunch of places I used `ceilf` and I needed to use `ceil` for 64-bit processors, since CGFloats are doubles on 64-bit. The other cases were similar (`floorf`/`floor`, `fabsf`/`fabs`). (I use `ceil` a bunch in layout code because I want to make sure view frames use integral values, and some things like text measurement return non-integral sizes.)

#### Toolbars

There are a two places where we use `UIToolbar`: in the detail view and in the web browser view. I like that the new `UIToolbar` is translucent, with a live-blurred background.

But I treat `UIToolbar` like any other view. In the past I’ve found that it’s difficult to precisely control the location and tap target size of buttons inside a `UIToolbar`, so now I just add buttons as subviews. I don’t particularly like doing that, but it works.

#### Gesture Recognizers

Vesper doesn’t use a `UINavigationController`, so we don’t get the automatic pan-to-go-back gesture. Apple provided a new gesture recognizer — `UIScreenEdgePanGestureRecognizer` — that allows us to handle pan-to-go-back ourselves. It’s a subclass of `UIPanGestureRecognizer`, as you’d expect. Easy to use.

We don’t, by the way, use `UISwipeGestureRecognizer` anywhere. This is because a swipe is just a gesture, while pans are direct manipulation.

#### My favorite new small thing

`- (CGFloat)tableView:(UITableView *)tableView estimatedHeightForRowAtIndexPath:(NSIndexPath *)indexPath;`

### Things I Didn’t Use (or didn’t use much)

#### Dynamic Text

iOS 7’s dynamic text feature is very cool — but it doesn’t support fonts other than the system font. We added a Typography screen to Vesper, so that you could change the font size and weight in the app (and even use small caps for titles).

The API for dynamic text returns a `UIFont`. I could have just grabbed the font size and used that with our custom font. But that would have been a hack, and it felt like we were solving a problem that’s really Apple’s problem to solve.

(I can see *why* dynamic text supports only the system font. But for apps that use custom fonts, it would still be useful to be able to get the user’s preferred font size.)

#### Dynamics and Motion Effects

It seems like Vesper is exactly the kind of app that should use dynamics and motion effects, and I certainly plan to in the future. But I already had working code to do the things we wanted to do, and there was no reason to rewrite that code.

I did write one parallax effect — see the image behind the sidebar. At first I made the rookie mistake of making the parallax move the reverse of what you’d expect. My designers caught it.

I’m looking forward to using this technology more. So cool.

#### Autolayout

We use autolayout in one small view in Vesper.

I’m still not sold on it. When I’ve used it, it doesn’t make for less code, and it does make for trickier debugging. I don’t like the way it interferes with animations. (Just animating to new frames doesn’t work — constraints have to be dealt with. Which makes sense, but I don’t like the extra work.)

And it’s not as if `layoutSubviews` is particularly hard

But still I have this itchy sense that autolayout is the future and I really need to adopt it. So I will, but incrementally.

#### Xibs and Storyboards

We use xibs only for the Credits screen, and I’ll probably change that to all code as soon as I get a chance.

I don’t recommend this route for every app. Vesper has very few screens and just about everything is custom. Xibs (and storyboards) don’t buy me anything. (But, again, that’s not true for every app. I don’t recommend going xib-less as a general rule.)

#### Core Data

What prevents me from using Core Data at this point is my concern for scalability and performance. It’s possible I’m just being thick-headed.

Likely, even.
