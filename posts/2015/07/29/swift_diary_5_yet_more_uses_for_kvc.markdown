@title Swift Diary #5: Yet More Uses for KVC
@pubDate 2015-07-29 10:03:12 -0700
@modDate 2015-07-29 10:45:14 -0700
I’ve argued before (<a href="http://inessential.com/2015/07/22/swift_diary_2_kvc">here</a> and <a href="http://inessential.com/2015/07/24/swift_diary_4_kvc_again">here</a>) that pure Swift objects and structs need KVC or something like it.

I keep running across real-world uses. I present two more.

#### Templates

In NetNewsWire you could create a custom theme, which was a CSS file, an HTML template, and, optionally, some assets.

Inside a template you could type things like <code>&#91;[newsItemTitle]&#93;</code>, and at render-time that string would be replaced with the title.

How this was done:

The template renderer took two objects:

1. A string — the template itself. (The thing that included some HTML and code like <code>&#91;[newsItemTitle]&#93;</code>.)

2. An object, typed as <code>id</code>.

The template renderer worked by scanning the template. Every time it found something in double-brackets — <code>&#91;[whatever]&#93;</code> — it pulled out the <code>whatever</code> part (call it the “tagName,” for lack of a better word) and got the replacement string like this:

<code>replacement = [obj valueForKey:tagName];</code>

Then it would replace <code>&#91;[whatever]&#93;</code> with the value of <code>replacement</code>.

What was cool about this was that the template renderer didn’t know anything about HTML or RSS. It didn’t know anything whatsoever about the passed-in object that generated the replacement strings. The system was uncoupled and reusable.

It knew how to scan through a string and replace <code>&#91;[something]&#93;</code> with a call to <code>valueForKey:</code>, and that’s it.

Would I love to be able to do the same thing with a Swift struct as the object? You bet. This is a great case for a struct.

#### Object Comparison and Updating

Say I’m writing an RSS reader or Twitter client — or something like Vesper or Glassboard — where the app makes calls to a web service to get a bunch of objects, then it compares those incoming objects to objects it already has and updates them as needed.

This code doesn’t have to be a pain to write. In fact, you can write it once and reuse it in every single app.

You need a comparison method that takes two objects — typed as <code>id</code> — and a set of property names to check.

<code>+ (void)updateExistingObject:&#8203;(id)existingObject withServerObject:&#8203;(id)serverObject propertyNames:(NSSet \*)propertyNames;</code>

Loop through propertyNames. For each:

<code>id oneExistingValue = [existingObject valueForKey:&#8203;onePropertyName];</code><br />
<code>id oneServerValue = [serverObject valueForKey:&#8203;onePropertyName];</code><br />
<code>if (![oneExistingValue isEqual:oneServerValue]) {</code><br />
<code>&nbsp;&nbsp;[existingObject setValue:oneServerValue forKey:&#8203;onePropertyName];</code><br />
<code>}</code>

Note that existingObject and serverObject don’t have to be the same type. serverObject could even be a dictionary. Whatever. It doesn’t matter, as long as the property names match up.

Also note that you could easily extend this to return a BOOL saying whether or not existingObject actually changed. This can be very useful if you need to conditionally save a database or plist or update the UI.

You can go a step further and have it return the set of property names that changed. If you have a custom persistence system, this could mean less work your database has to do when updating existingObject in the database. (For instance: you could generate SQL that updates the values only for those changed property names.)

This is also just a few lines of code away from a syncing system [like the one in Vesper](http://inessential.com/vespersyncdiary). In Vesper the various properties have a modification date property. (For instance: note.text and note.textModificationDate.)

The above code would be modified like this:

1. In the case where values aren’t equal, it then constructs the modification date property name from the property name (by appending <code>@"ModificationDate"</code>, so that you have textModificationDate and similar).

2. Then it does <code>valueForKey:</code> on both objects to get that date. It compares the dates. Whichever value has the later date is the winning value.

And then you could write 100 apps that all use this same code.

(To bring it back to Swift: serverObject ought to be a struct.)

#### Trade-offs

The compiler isn’t going to catch some possible errors. But I’m willing to put up with that because of the other benefits — these systems are uncoupled and highly reusable, and they mean <em>writing and maintaining less code</em>.

I don’t suggest for one second that KVC should be used everywhere and all the time. I <em>love</em> having the compiler catch bugs. But there are often some small-but-important spots like these where KVC is the best choice.

#### Update 10:25 am

I had thought it was obvious, but beyond the scope of this post, to point out that in the first pattern you need some constraints and you need to handle undefined keys.

This is pretty easily done. The object that generates replacement strings could be a dictionary. Or you could override valueForKey and valueForUndefinedKey. That object certainly should not have any methods other than what’s needed to generate the replacement strings.

In the end you might think it’s safer to base the system entirely on dictionaries and use objectForKey instead (especially when there’s a chance that the templates include user data). Totally fair.
