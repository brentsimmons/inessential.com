@title Print Numbers to the Console Painlessly with this One Weird Trick
@pubDate 2014-11-25 15:01:15 -0800
@modDate 2014-11-25 15:01:15 -0800
I’ve given up trying to remember NSLog number formatters. I was cool with it until Macs got 64-bit processors — and then I just lost it when I stopped being able to use <code>%d</code> most of the time.

And now I’ve given up even looking up the number formatters. With the new literals syntax it’s just so easy — as in this line of code I just wrote:

<code>NSLog(@"t: %@", @([d2 timeIntervalSinceDate:d]));</code>

What did I want? <code>%f</code>? I don’t need to know or care.
