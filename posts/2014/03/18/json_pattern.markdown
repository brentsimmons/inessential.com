@title JSON Pattern
@pubDate 2014-03-18 12:31:55 -0700
@modDate 2014-03-18 12:38:29 -0700
I’m not sure I have the best pattern for serializing and de-serializing model objects as JSON.

I’ll describe what I have.

#### QSAPIObject Protocol

Some (but not all) of my model objects can be represented as JSON. Those model objects are not subclasses of anything (by design) — but they do implement a couple protocols, including the QSAPIObject protocol.

This protocol requires two methods:

<code>- (NSDictionary \*)JSONRepresentation;</code><br />
<code>+ (instancetype)objectWith&#8203;JSONRepresentation:&#8203;(NSDictionary \*)JSONRepresentation;</code>

This part makes sense, I think. There’s no shared code in JSON serialization/deserialization, so it makes sense as a protocol as opposed to a subclass.

But here’s where it gets tricky.

#### Collections

I want some common code to handle arrays — I want JSONArrayWithObjects and objectsWithJSONArray.

These methods are exactly the same for all model objects: they create an array, and populate it by calling the QSAPIObject protocol methods.

What I did: I created a QSAPIObject class (in the same file as the protocol with the same name) and gave it two class methods:

<code>+ (NSArray \*)JSONArray&#8203;WithObjects:(NSArray \*)objects;</code><br />
<code>+ (NSArray \*)objectsWith&#8203;JSONArray:&#8203;(NSArray \*)JSONArray class:(Class&lt;QSAPIObject&gt;)class;</code>

So, to turn VSNote objects into JSON dictionaries, I do this:

<code>NSArray \*JSONNotes = [QSAPIObject JSONArrayWithObjects:&#8203;notes];</code>

And to turn JSON dictionaries into VSNote objects:

<code>NSArray \*notes = [QSAPIObject objectsWithJSONArray:&#8203;JSONArray class:[VSNote class]];</code>

This isn’t the worst thing. It works perfectly well. But I don’t particularly love calling class methods — why not just make them C methods?

<code>NSArray \*JSONNotes = QSJSONArrayWithObjects(notes);</code>

As C methods, there’s one entity (a function name) rather than two (class and method), and I like that. But, on the other hand, using C methods for things like this can be considered a code smell — it’s a sign that we’ve stepped outside of our object-oriented world. (Same with class methods, but with C it’s more obvious.)

Another thing I don’t like is that class parameter to objectsWithJSONArray. That’s a dead give-away that something’s gone wrong here in object-land.

I could add these collection methods to the QSAPIObject protocol, and make the model objects implement these. Then I’d have something nicer like:

<code>NSArray \*notes = [VSNote objectsWithJSONArray:&#8203;JSONArray];</code><br />
<code>NSArray \*JSONNotes = [VSNote JSONArray&#8203;WithNotes:&#8203;notes];</code>

That’s a more ideal API, for sure. But then the model objects are duplicating code — unless those methods are just one-liners that call the common implementations in the QSAPIObject class methods.

And if I do that, I’m basically adding boilerplate code to my model objects that isn’t strictly necessary, that would be there just so I could feel a little better about the API. Calling the QSAPIObject class methods is perfectly work-able, if un-lovely.

Hmmm.
