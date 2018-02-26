@title Fetching Objects with FMDB and SQLite
@pubDate 2014-03-26 15:59:48 -0700
@modDate 2014-03-27 12:07:51 -0700
(Experienced developers know all this stuff. If that describes you, you can skip this post.)

Say you’re crazy — which is not recommended, but it could happen — and you want to write your own data layer. One way to do that is to write very specific code that you could never reuse.

A better way is, of course, to write generic, reuseable code. But how do you do that with [FMDB](https://github.com/ccgus/fmdb) and SQLite? How do you make it so the data layer can work with *any* object?

It’s pretty easy, actually.

#### Simple, Non-generic Example

Let’s say you have a `BSPerson` object with the following properties:

<code>@property (nonatomic, assign) int64_t uniqueID;</code><br />
<code>@property (nonatomic) NSString *name;</code>

You’ve created the table in your SQLite database with something like this:

<code>CREATE TABLE if not exists people (uniqueID INTEGER UNIQUE NOT NULL PRIMARY KEY, name TEXT NOT NULL);</code>

To fetch that object by its uniqueID, you’d use an `FMDatabaseQueue` and code like this:

<code>FMResultSet *rs = [database executeQuery:@"select * from people where uniqueID=?;" @(uniqueID)];</code>

(Note that `uniqueID` is boxed, since FMDB wants objects.)


Then loop through the result set — there’s just one result in this case, but you might have multiple results and you’d create an array of results. But we’ll stick to one to keep this simple.

<code>BSPerson \*person = [BSPerson new];</code><br />
<code>while([rs next]) {</code><br />
<code>&nbsp;&nbsp;person.oneUniqueID = [rs longLongIntForColumn:@"uniqueID"];</code><br />
<code>&nbsp;&nbsp;person.name = [rs stringForColumn:@"name"];</code><br />
<code>}</code>

That’s super-specific, right? The code knows about `BSPerson` and its properties.

#### Reusable Example

First let’s make BSPerson more complex. We’ll add two properties:

<code>@property (nonatomic) NSDate \*birthDate</code><br />
<code>@property (nonatomic) NSData \*imageData;</code>

The object creator needs some information: it needs the class of the object and some properties information. You could get this information a few different ways (in code or convention, or you could write a JSON or plist file that gets turned into a dictionary).

Let’s say the properties dictionary looks like this:

<code>@{@"uniqueID" : @"int64", @"name" : @"string", @"birthDate" : @"date", @"imageData" : @"data"}</code>

And of course the class is <code>[BSPerson class]</code>. Pass the class and dictionary to the object creator as `objectClass` and `properties` and you can do this (after the executeQuery):

<code>id oneObject = nil;</code><br />
<code>while([rs next]) {</code><br />
<code>&nbsp;&nbsp;oneObject = [self objectOfClass:objectClass withRow:rs properties:properties];</code><br />
<code>}</code>

(Yes, again I’m assuming a single-row result set, just for the sake of simplicity. Making an array is hardly any additional code.)

`objectOfClass` looks like this:

<code>id oneObject = [objectClass new];</code><br />
<code>&nbsp;</code><br />
<code>for (NSString \*oneProperty in properties) {</code><br />
<code>&nbsp;</code><br />
<code>&nbsp;&nbsp;NSString \*oneType = properties[oneProperty];</code><br />
<code>&nbsp;&nbsp;id oneValue = nil;</code><br />
<code>&nbsp;</code><br />
<code>&nbsp;&nbsp;if ([oneType isEqualToString:@"date"]) {</code><br />
<code>&nbsp;&nbsp;&nbsp;&nbsp;oneValue = [rs dateForColumn:oneProperty];</code><br />
<code>&nbsp;&nbsp;else {</code><br />
<code>&nbsp;&nbsp;&nbsp;&nbsp;oneValue = [rs objectForColumnName:oneProperty];</code><br />
<code>&nbsp;&nbsp;}</code><br />
<code>&nbsp;</code><br />
<code>&nbsp;&nbsp;[oneObject setValue:oneValue forKey:oneProperty];</code><br />
<code>&nbsp;&nbsp;}</code><br />
<code>&nbsp;</code><br />
<code>return oneObject;</code><br />

(Note: you wouldn’t really use `@"date"` and so on as literals — you’d define constants. Of course. And you might think twice about storing image data in a database. This is all just for illustration.)

A few things to note:

* Even though BSPerson’s uniqueID property is *not* an object, <code>setValue:forKey:</code> does the right thing. The function is getting an object from the FMResult, but setValue:forKey: knows to set it as an int64_t, because that’s how the property is defined. This is cool. Very, very cool. (Similarly, you could have an integer in the database that goes to a BOOL property.)

* FMResultSet’s `objectForColumnName:` handles integers, floats, blobs, and strings. The one thing to watch out for is dates. If you never have any dates, you could probably get away without having a properties dictionary — you could just use an array of property names and rely on `objectForColumnName:`. Or you could define a convention where a property name ending in “date” is always an NSDate property.

* You could extend the type system — you might have plist and archived types where your code automatically serializes and deserializes the values. It’s best to avoid this, but it can be useful, sparingly.

It’s tempting to want to use property introspection — via `class_getProperty` and `property_getAttributes` — instead of specifying types explicitly or via convention. I haven’t done this, and I tend to shy away from runtime functions. However, this could be a case where it’s useful and warranted. You couldn’t assume that every property has a corresponding column, but you could check the column names (which you can get) against the corresponding properties to see when you have an NSDate.
