@title Immutable Objects and Calculated Properties
@pubDate 2014-03-21 14:34:23 -0700
@modDate 2014-03-21 14:34:23 -0700
I didn’t think about calculated properties in my recent post on [immutable objects](http://inessential.com/2014/03/20/immutable_model_objects).

I suspect I’m not alone in never feeling all that great about calculated properties. You either calculate them on-demand every time — which is fine if performance is not an issue and you don’t need to make them observable — or you calculate them when the data they depend on changes.

The latter is a pain and requires some special fiddling with KVO, notifications, custom accessors, and so on. (Do Core Data users use awakeFromInsert and awakeFromFetch? I always avoided this particular topic with Core Data.)

Not that it’s all that hard. I just don’t like that particular code.

But with immutable objects, it’s so simple: calculate on-demand just once. Since the data doesn’t change, there’s no need to set up recalculation machinery. So clean.
