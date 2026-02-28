@title Why Objective-C
@pubDate 2026-02-27 17:21:48 -0800

[In my previous post](https://inessential.com/2026/02/18/why-not-objective-c.html) I talk about how I got rid of hundreds of thousands of lines of Objective-C code while at Audible and I explain *why* keeping Objective-C code around is a terrible idea. And I explain that…

> I’m not stuck in the old ways; I’m not the guy insisting on the supremacy of Objective-C despite the obvious evidence against. I’m the guy who got rid of Objective-C — with glee and (oops, sorry Audible marketing team for the screwup) wild abandon!

Then of course I wrote some Objective-C code recently and really, really loved it.

### Command line app

I wanted to replace my homegrown static website/blog generator because I no longer wanted to use the language it was written in, for reasons.

I took it as a good opportunity to learn Python — but it turned out that my heart wasn’t in it (not Python’s fault; great language) and I ended up screwing it up. (See [Blog Fuckup](https://inessential.com/2026/02/01/blog-fuckup.html)).

I thought about some alternatives: Swift, which I know well; Rust and Go, which would have the advantage of helping me branch out from the Apple ecosystem; and good old C, my happy-go-lucky friend who still sprints faster than every brash new language.

Of those I was leaning toward C because speed is an issue. I wanted to make rendering this blog, over 25 years old and with thousands of posts, to happen in under one second. The system I was replacing took a few seconds. But I wanted more speed (personality flaw).

And then I thought, I swear just for a split second, about how great it would be if C had something a little nicer than C structs for modeling my app’s data — and oh well too bad there’s nothing like that.

And then I remembered Objective-C, which is C plus some things a little nicer than C structs. 🎩🦖

### Objective-C looks insane

Anyone new to Objective-C thinks it’s difficult and maybe a bit harsh because `[[those squareBrackets] lookInsane:YES]`.

Once you get past that, which takes a day or two given a good-faith effort, you’ll realize how small a language it is, how easy to hold in your palm and turn it around and understand all sides of it. And you’ll appreciate how easy it is to make good decisions when you don’t have a surplus of language features to choose from.

And you’d be reassured to know that Objective-C is probably never going to change, which means tech debt will accumulate much more slowly than with newer languages. (Unless, of course, you count Objective-C itself as tech debt. You don’t have to, though.)

It’s a cliché to call Objective-C a more elegant weapon for a more civilized age. It’s better thought of, these days, as a loaded footgun.

But I did absolutely love writing this code! So much fun. And now I’ve got another little thing brewing, also in Objective-C, coming soon-ish.

PS [The website/blog generator app is called SalmonBay](https://codeberg.org/brentsimmons/SalmonBay). I really don’t expect anyone else in the world to use it, and I expect no contributions, but it is available as open source. (I put it on Codeberg, for reasons.)

PPS SalmonBay does a clean build of this blog in under a second. 🎸
