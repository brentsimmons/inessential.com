@title NetNewsWire CI, New Technote
@pubDate 2019-06-12 22:09:39 -0700
@modDate 2019-06-12 22:09:39 -0700
We now have continuous integration set up for NetNewsWire. I didn’t need it for a long time, when it was just me — but now that we have multiple contributors, it’s important. 

We’re doing the app *and* the separate frameworks (RSCore, RSParser, etc.) the app uses.

Thanks to [circleci](https://circleci.com/) for the service and to [Joe Heck](https://rhonabwy.com/) for setting it all up!

<p style="text-align:center">* * *</p>

Most of my work, between now and shipping, is writing. Here’s a new technote: [Why Reruns Happen](https://github.com/brentsimmons/NetNewsWire/blob/master/Technotes/Reruns.md).

<p style="text-align:center">* * *</p>

We have had not one single crash report since 5.0a3 shipped. :)

(Yes, the app does have a crash catcher: no, we’re not relying on people finding the crash logs on disk and sending them in.)
