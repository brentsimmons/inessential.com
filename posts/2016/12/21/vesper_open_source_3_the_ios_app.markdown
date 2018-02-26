@title Vesper Open Source #3: the iOS App
@pubDate 2016-12-21 12:30:51 -0800
@modDate 2016-12-21 12:31:06 -0800
<a href="https://github.com/brentsimmons/Vesper">Vesper for iOS is up on GitHub</a>.

It’s presented as a historical artifact rather than as a living project. It’s definitely not an example of how to write apps these days — and it’s not even an example of how to write apps in 2013.

There are good parts and bad parts, embarrassing parts, parts that clearly need refactoring, etc. etc.

The only changes from the code in our current repository were to remove the incomplete Mac app code, remove Hockey, remove Ideal Sans (the embedded font), make a few code changes related to switching to the system font, and get it to compile with Xcode 8.2.1.

#### Surprisingly Big

It’s been a while since I lived in this code and, coming back to it, I was struck by how very much code there is. It’s a little nuts. This is just a note-taking app, after all.

If you remember the context, though, it’s perhaps not that surprising.

It was written while iOS 6 was current, and it still looks like an iOS 6 app under the hood. But, at the same time, we were anticipating iOS 7, and so Vesper was an art project — we wanted Vesper to join Letterpress and Twitterrific and a few others as one of the first Modernist apps.

But we hadn’t actually *seen* iOS 7, and so we invented Vesper’s look and feel from scratch, though with some idea of where the puck was heading. That — combined with wanting to use Ideal Sans everywhere, even in standard things like alerts — meant we had to do a ton of custom UI and animations.

It’s interesting to me that 2013 was about the last time you could plausibly think that that’s the right thing to do. It’s clearly too expensive now — and was too expensive then, too, but we hadn’t realized it yet.

The irony is that we thought Vesper was one of the first apps of a new era — the era that officially kicked-off with iOS 7 — but, in the end, it was one of the last apps of the era where it was not uncommon for developers to spend massive amounts of time in UI invention.

It’s a different era now. I don’t mean that critically — iOS 7 and the follow-ups have brought iOS closer to where the Mac has been all these decades, where you have standard system UI that’s good and that doesn’t require much customization. That’s a good thing.

Were we to write Vesper *now*, based on that same initial idea (drag to reorder plus tags), we’d do it in far less code. (I’d guess it would take about a third of the code.) But would we still use Ideal Sans? I bet we would. What a lovely font. I regret that we couldn’t provide it in the open source version.

#### Forking

You’re welcome to do whatever you want with Vesper for iOS as long as you respect the license (MIT). Also: the name Vesper and the app icon remain the property of me, Dave, and John.

However: everything I said above is true. Under the hood it’s an iOS 6 app. You really should treat it as history. There may be lessons to learn — what *not* to do as well as what *to* do — but I don’t recommend using it as the basis for a new app.

#### More blog posts

There are specific things in Vesper worth writing about. There will be more posts. (Though probably not today. It’s sunny in Seattle! I’m going outside.)
