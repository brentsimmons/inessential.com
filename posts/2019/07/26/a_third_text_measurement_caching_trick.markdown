@title A Third Text Measurement Caching Trick
@pubDate 2019-07-26 15:16:43 -0700
@modDate 2019-07-26 15:16:43 -0700
I forgot about this one — I should have mentioned it in the [previous article](https://inessential.com/2019/07/26/a_couple_handy_tricks_for_text_measureme).

Let’s say the source text that gets displayed in your timeline could be quite long. NetNewsWire has this issue: the summary text is the text of an article (with HTML tags stripped).

This text could be many thousands of words long. But the timeline will only ever display at most a couple lines — even with an absurdly wide timeline on a large screen, it will never display thousands of words.

So here’s the trick:

Use a truncated version of the text rather than the entire text. For the truncation limit, come up with a length that is beyond what could conceivably fit in the space.

This way text measurement will be faster since it’s measuring less text.

(Also use this truncated text for the text field in the timeline.)
