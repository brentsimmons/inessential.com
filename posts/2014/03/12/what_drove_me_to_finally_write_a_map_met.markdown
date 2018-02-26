@title What Drove Me to Finally Write a Map Method
@pubDate 2014-03-12 17:02:45 -0700
@modDate 2014-03-12 17:04:12 -0700
I try to add category methods sparingly, on the principle that creating my own personal dialect of Cocoa is a bad idea. (That’s not to say I never do. [Here are some](https://github.com/quartermaster/QSKit/tree/master/Classes/Foundation).)

Much of the time I can get by without a map method by using either `valueForKeyPath:` or <code>filteredArray&#8203;UsingPredicate:</code>.

But today I ran across one that required *both* methods.

I have an array of notes (for Vesper’s timeline). Each note has a `thumbnailID` property — which is nil when there’s no thumbnail.

I wanted an array of non-nil thumbnailIDs.

I could get all the thumbnailIDs, including nils, which turn into NSNulls, with `valueForKeyPath:`.

<code>NSArray *thumbnailIDs = [notes valueForKeyPath:&#8203;VSThumbnailIDKey];</code>

And then I could get non-nil thumbnailIDs:

<code>NSArray *thumbnailIDsMinusNulls = [thumbnailIDs filteredArray&#8203;UsingPredicate:&#8203;[NSPredicate predicateWithFormat:&#8203;@"SELF != nil"]];</code>

And that’s not *terrible*. But I looked around for a better way and didn’t find anything. So I finally broke down and wrote a map method.

So now the code looks like this:

<code>NSArray \*thumbnailIDsMinusNulls = [objects qs_map:^id(id obj) {</code></br>
<code>&nbsp;&nbsp;return ((VSTimelineNote \*)obj).thumbnailID;</code></br>
<code>}];</code>

If `thumbnailID` is nil, the block returns nil and it doesn’t get added to the array.

The map function (in an NSArray category) looks like this:

<code>typedef id (^QSMapBlock)(id obj);</code>

<code>- (NSArray \*)qs_map:(QSMapBlock)mapBlock {</code></br>
<code></code></br>
<code>&nbsp;&nbsp;NSMutableArray \*mappedArray = [NSMutableArray new];</code></br>
<code></code></br>
<code>&nbsp;&nbsp;for (id oneObject in self) {</code></br>
<code></code></br>
<code>&nbsp;&nbsp;&nbsp;&nbsp;id objectToAdd = mapBlock(oneObject);</code></br>
<code>&nbsp;&nbsp;&nbsp;&nbsp;if (objectToAdd) {</code></br>
<code>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[mappedArray addObject:objectToAdd];</code></br>
<code>&nbsp;&nbsp;&nbsp;&nbsp;}</code></br>
<code>&nbsp;&nbsp;}</code></br>
<code></code></br>
<code>&nbsp;&nbsp;return [mappedArray copy];</code></br>
<code>}</code>

It’s surprising to me that there isn’t a built-in map method for NSArray. I may be the last Cocoa programmer to write my own.
