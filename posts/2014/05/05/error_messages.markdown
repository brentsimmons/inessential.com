@title Error Messages
@pubDate 2014-05-05 11:20:43 -0700
@modDate 2014-05-05 11:21:48 -0700
I can’t find a note specifically about error messages in either the [iOS](https://developer.apple.com/library/ios/documentation/userexperience/conceptual/MobileHIG/index.html) or [Macintosh Human Interface Guidelines](https://developer.apple.com/library/mac/documentation/UserExperience/Conceptual/AppleHIGuidelines/Intro/Intro.html). (Maybe I just missed it.)

There is, however, old wisdom — perhaps from an earlier version of the Mac HIG — that says how to create error messages: they should be of the form “Can’t x because of y.”

They may optionally include additional detail and/or recovery steps. “Can’t x because of y. Something is true. Try a thing.”

(Best case is when there’s a button that lets you try that thing without having to do it manually.)

A similar form is this: “Noun can’t x because y.” (As in “‘Downloaded.app’ can’t be opened because it is from an unidentified developer.”)

One thing error messages never say is <em>sorry</em>. They’re just reporting, and they respect you enough to know you want the facts, clearly expressed, and don’t need to be apologized-to by a machine.

Also: they rarely (if ever) use the words I, me, my, you, and your.

[HAL 9000](https://www.youtube.com/watch?v=ARJ8cAGm6JE&app=desktop), were it a Mac, would report: “Can’t open the pod bay door because this mission can’t be jeopardized.” Or: “The door ‘Pod Bay’ can’t be opened because it would jeopardize this mission. Try the emergency airlock.”

I think it’s worth keeping this in mind when writing error messages, but also note that there may be some exceptions. I haven’t thought it all the way through, but a couple things come to mind.

* Form-field validation errors. I think you want something succinct next to the field rather than a full “Can’t submit this form because blah” error.

* iOS and space constraints. There may not be enough room for a classic error message. Of course, this may mean that the design should be revised until there is room — but that may mean a worse trade-off.
