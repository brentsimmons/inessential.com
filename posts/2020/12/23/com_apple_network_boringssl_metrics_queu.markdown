@title Apple’s SSL Metrics Is Hanging My App
@pubDate 2020-12-23 14:16:21 -0800
@modDate 2020-12-23 14:17:57 -0800
We’ve been getting some reports that NetNewsWire for Mac will hang sometimes. A sample will report something like this:

	Dispatch Thread Hard Limit: 512 reached in 1580 of 1580 samples -- too many dispatch threads blocked in synchronous operations

And there will be hundreds of threads labelled `com.apple.network.boringssl.metrics_queue`.

[Here’s an example](https://github.com/Ranchero-Software/NetNewsWire/issues/2671), with sample report, on our bug tracker.

What I think is happening: these Apple metrics reports are happening once per download per feed. So, if you have 1,000 feeds, then there are 1,000 metrics reports for a given download session. If those reports don’t complete quickly enough, then you get this thread explosion.

So… I could slow down our feed downloader so that this is less likely to happen, so that the metrics reports don’t back up so much. I don’t really want to slow down refreshing, though, but I may have no choice.

Luckily, most people don’t have the number of feeds it would take to trigger this. But, still, that’s not good enough — NetNewsWire should never hang for any user.
