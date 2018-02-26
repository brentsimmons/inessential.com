@title Introduction to Ballard

(Note: this document is from an alternate universe where, instead of [porting Frontier](http://inessential.com/frontierdiary), I started from scratch on a new app inspired by Frontier.)

This article is for programmers who want to know how Ballard, the scripting language for $APPNAME, is like other languages and how it’s different. See the website for tutorial articles for people new to programming.

(Yes, the app has no name. It’s $APPNAME for now.)

But, before we get into things, let’s get this out of the way first — the following is a valid Ballard script:

	var 🐥 = 'I believe in example'

## Where it comes from

Ballard descends from UserTalk, the scripting language for UserLand Frontier. It borrows from other languages — Swift and JavaScript, especially.

It’s not an object-oriented language — it’s *table*-oriented.

The idea behind Ballard — which is lifted completely from UserTalk — is the integration of the scripting system and a persistent database. The database is made up of tables that can contain other tables, which contain other tables, and so on. Names of tables, and the objects they contain, become symbols in the language.

Tables are like dictionaries in other languages. Tables contain name/value pairs. There is no schema: any table can contain anything. The keys are always strings.

(Note: the database is often called an object database, or odb, even though it doesn’t contain objects in the object-oriented sense. It contains objects in the sense that they’re things, but “object” sounds better.)

The language uses dot notation to denote paths. If you have a string name "foo" stored in a table "prefs" stored in a table "user", then you can set that value like this:

	users.prefs.foo = 'candles'

If user.prefs.foo didn’t exist, it would be created. If it already existed, it would be replaced.

The point is to make persistence as simple as possible.

We know from years of experience with UserLand Frontier that this integration is a powerful aid to rapid prototyping, iteration, and development — particularly when combined with a desktop app where you can browse and edit the database. It promotes exploration and experimentation. It makes scripting *fun*.

Ballard emphasizes internet scripting. What AppleScript is to scriptable Mac apps, Ballard is to the internet. However, Ballard also works very well with scriptable Mac apps, the file system, and so on. The idea is to bridge those two worlds, the internet and the local computer.

## Language Goals

From most important to least important:

1. It should make persistence easy, natural, and readable.

2. It should be possible to be highly productive. This means a minimum of housekeeping, and it means things like dynamic types and automatic coercions. When the language can infer what you meant, it will.

3. The syntax must work great in an outliner.

4. It should be easy to learn for both JavaScript and Swift programmers. (Ideally, both sets think the language is actually descended from their language.)

## Types and Values

Ballard is dynamically typed. The following is perfectly legal:

	var x = "some string"
	x = 3.14592
	x = [6, 'another string', [5, 4]]
	
A given variable — or object in the database — can change its type just by assigning it a new value:

	user.prefs.foo = 9

Functions don’t declare types in their parameter lists; functions don't declare a return type.

Ballard supports the following types: booleans, nil, integers, doubles, dates, strings, binary data, arrays, tables, outlines, and scripts.

### Everything except for tables is passed by value

For example:

	var x = 'foo'
	var y = x
	y = 'bar' // x is still 'foo'
		
If you then call `someFunction(x)`, then someFunction will get a copy of x.

(Note: copies are massively cheap. In most cases no actual copy is made, since the under-the-hood value objects are immutable.)

#### But you can pass by reference

There is an escape hatch: addresses. You can pass the address of a local variable or object in the database to a function.

	var s = 'some string'
	someFunction(@s)
	
	def someFunction(adrString)
		adrString^ = 'another string' // s from the calling function is now 'another string'
		
Note the syntax: the @ character signifies an address; the ^ character de-references the address. (Note to Frontier users: this syntax is rarely used in Ballard as compared to UserTalk, mainly because tables are passed by reference, which is a major change from Frontier. See below.)

Also note that functions are defined using the `def` keyword, which is short for “function definition.”

### Tables are always passed by reference

Tables can be complex and arbitrarily large, with any number of sub-tables. And much of the time you will be working with tables that persist in a database rather than as local variables. For those two reasons it makes sense to pass tables by reference rather than by value.

	def updateModificationDate(t)
		t.modificationDate = date.now()
	updateModificationDate(user.prefs)
	// user.prefs.modificationDate is now the current date

This also simplifies the syntax. If tables were pass-by-value, you’d have to use the address of the table and then dereference it, as (Frontier users will remember) you did have to do in UserTalk:

	on updateModificationDate(adrTable)
		adrTable^.modificationDate = clock.now()
	updateModificationDate(@user.prefs)
	// user.prefs.modificationDate is now the current date

Even though treating tables differently than other types means added complexity (compared to UserTalk), we think it ends up simpler and more natural. Our bet is that this is how you’d expect it to work. (In other words, we believe you don’t want to type `adrTable^` and `@user.prefs`: you prefer the first example over the UserTalk example.)

If for some reason you *do* want to copy a table, you can: `var t = table.copy(some.other.table)`. It does a deep copy of everything in the table: everything inside the table is copied also. For small tables this is fast (because copies of everything that isn’t a table are cheap).

### Semicolons and curly braces

The above examples don’t include semicolons. Line feeds take the place of semicolon. A semicolon is a syntax error.

Code blocks, however, do take curly braces:

	if user.prefs.foo == 'some string' {
		user.prefs.foo = 50
	}

However, $APPNAME’s code editor is an outliner. Because you indent code in an outliner, the outliner knows where the braces should go, and hides them. So you’ll actually see the above code like this:

	if user.prefs.foo == 'some string'
		user.prefs.foo = 50

That does *not* mean that Ballard looks at whitespace the way Python does. It just means that Ballard’s code editor automatically inserts braces behind the scenes before passing to the compiler.

Since you are most likely to write code in $APPNAME’s editor, this guide leaves out the braces. If you’re writing code in another editor, you might need to add braces. (They go in the logical places.)

Note: as you’re reading this, $APPNAME might not exist yet. If you’re using BSE (Ballard Script Editor) — which is a text-view-based editor — you *do* need to include the semicolons.

### Variables

Ballard borrows from Swift the use of `var` and `let` as ways to distinguish mutable and immutable variables. Use of `let` is encouraged, as immutability is encouraged.

	var x = users.prefs.foo, y = 100.0
	let z = 'this can’t be changed'
	z = 500 // This is an error!

(Note: Ballard does not borrow the concept of optionals from Swift, as that feature imposes more housekeeping than is warranted for a scripting language.)

`let` in Ballard goes a little bit farther than it does in other languages. If a variable is declared using let, and it’s a reference type (a table), the referenced object can’t be mutated. For example:
	
	let x = user.prefs.foo // user.prefs.foo is a table
	x.bar = "a string" // This is a runtime error.

### Functions

A script can include one or more functions, and a function may contain other functions.

Functions are declared using the keyword `def` followed by a name (optionally) followed by a parameter list. Examples:

	def someFunction(x, y, z)
	def(x, y, z)

When calling a script stored in the database, the system looks inside that script for a function that matches the name of the script. If not found, it looks for the first function with no name.

For example, a script stored at workspace.myScript might look like this:

	def myScript(s)
		msg(s)

If you change the database location from workspace.myScript to workspace.myMessageScript, you’d also have to edit the function declaration to `def myMessageScript(s)`.

However, if the function declaration is `def (s)` — no function name — then you can rename the script without having to edit the function declaration.

Note: a script need not define a function at all. It can then be called with no parameters. If the following script lived at workspace.myScript, you’d just call `workspace.myScript()`.

	msg('Hello from workspace.myScript.')

Also: if a script defines top-level functions that don’t match its key in the database, and the script has top-level code, then the top-level code is called.

Though this sounds like a complex rule, in practice it’s intuitive. If workspace.myScript is the following:

	def callback(key, item)
		msg(item)
	table.visit(user.prefs, callback)

Then you’d call it as `workspace.myScript()`. The first line it would execute is the table.visit line, which is top-level code, as you’d expect.

However, if a script has top-level code *and* an appropriate top-level function (either anonymous or with a name matching the database key), then calling the script calls the appropriate top-level function.

	def (someTable)
		def callback(key, item)
			msg(item)
		table.visit(someTable, callback)
	this(user.prefs)

(The keyword `this` refers to the currently-running script object).

Calling `workspace.myScript(aTable)` would skip the `this(user.prefs)` line, since it found a matching top-level function.

However — if you’re editing the script, and click the Run button (which means you’re not calling the script from elsewhere), then the top-level code is always executed. It starts with the `this(user.prefs)` line.

This is very useful when working on a script. You can include top-level code that isn’t run when the script is called from elsewhere, but that *is* run when you click the Run button.

The convention is to place that top-level test code at the bottom of the script, and enclose it in a `bundle` block. (A `bundle` is a convenience for creating a block of code that defines a scope.)

You’d write this:

	def (someTable)
		def callback(key, item)
			msg(item)
		table.visit(someTable, callback)
	bundle // test code
		this(user.prefs)

Clicking the Run button causes the bundle block to be executed, since the bundle is top-level code. But calling the script from elsewhere causes the top-level function to be executed, and the bundle is ignored.

Note: bundles can be used in other places too. It can be a handy code-organizing tool.

### Inner Functions

Functions may contain inner functions, and those inner functions see variables from the outer scope.

Say you wanted to generate a list of links from an array of URLs:

	def (urls)
		var htmlText
		def add(s)
			htmlText = htmlText + s
		def addLink(url)
			add('<a href=')
			add(url)
			add('>')
			add(url)
			add('</a>')
		for oneURL in urls
			addLink(oneURL)
		return htmlText

### Functions and optional parameters

A function can declare optional parameters by providing a value for those parameters:

	def someScript(x, y="foo", z=user.prefs.birthMonth)

You could call someScript with `someScript(10)` or `someScript(20, "bar")` or `someScript(30, "baz", "March")`.

### Functions and named parameters

Consider this function declaration:

	def someScript(x, y, z)

You can use the variable names as parameter names when calling, as in `someScript(z:10, x:'some string', y:someValue)`. When calling a function using named parameters, all the parameters must be named. Order doesn’t matter.

If someScript had declared optional parameters:

	def someScript(x, y="foo", z=user.prefs.birthMonth)
	
You could call it as `someScript(x:10)` or `someScript(z:"March", x:10)` and so on.

When scripting with Ballard, using descriptive names for variables is encouraged — and this is encouraged even more when naming parameters to a function. This helps make the calling functions more readable.

For instance, you might call the download verb like this:

<pre>let requestHeaders = ('User-Agent': 'My Cool App 1.0')
let result = download&#8203;(url:'http://inessential.com/&#8203;xml/rss.xml', headers:requestHeaders)</pre>

### Closures

To run a function for all items in the workspace.lyrics.pixies table, you might write something like this:

<pre>def callback(key, item)
	msg(item)
table.visit(workspace.&#8203;lyrics.&#8203;pixies, callback)</pre>
	
`table.visit` takes two parameters: a table, and a function to call with each item in the table. That function should take two parameters (the key, always a string, and the item).

Multiple closures or functions may be passed-in:

	def callback1(item)
		msg(item)
	def callback2(x, y)
		msg(x + y)
	def callback3()
		msg("Hello from callback3")
	someScript(someValue, callback2, callback3, callback1)

### Trailing closure syntax

Ballard also supports trailing closures. So you could call `table.visit` like this:

<pre>table.visit(workspace.&#8203;lyrics.&#8203;pixies), def (key, item)
	msg(item)</pre>

The `def (key, item)` declares the parameter list. It doesn’t need a function name, though you can give it a name if you like. The indented code is the body of the closure.

Consider the case where the function call is part of an if statement:

<pre>if table.visit(workspace.&#8203;lyrics.&#8203;pixies), def (key, item)
	msg(item)
	msg("table.visit ran and returned true.")</pre>
		
This is ambiguous, because you can’t tell when then the closure ends and the body of the if block starts. And so trailing closure syntax is not supported in the above. Instead you’d do something like this:

<pre>if table.visit(workspace.&#8203;lyrics.&#8203;pixies, displayItemCallback)
	def displayItemCallback&#8203;(key, item)
		msg(item)
	msg("table.visit ran and returned true.")</pre>

This is also legal:

<pre>table.visit(workspace&#8203;lyrics.&#8203;pixies, displayItemCallback)
	def displayItemCallback&#8203;(key, item))
		msg(item)</pre>

Closures, like inner functions, have access to the variables from the outside scope. The generating-links example could be written like this:

	def (urls)
		var htmlText
		def add(s)
			htmlText = htmlText + s
		array.visit(urls), def (url)
			add('<a href=')
			add(url)
			add('>')
			add(url)
			add('</a>')
		return htmlText			

### String Interpolation

You can create strings via addition `'foo' + 'bar'` — or you can use string interpolation instead. The generating-links example might look like this:

	def (urls)
		var htmlText
		def add(s)
			htmlText = htmlText + s
		array.visit(urls), def (url)
			add('<a href=\(url)>\(url)</a>')
		return htmlText			

Note: you can also enclose strings with &#92;" characters. String interpolation works with both &#92;' and &#92;" styles — that way you don’t have to remember which is which.

### Strings

Strings are Unicode strings.

	string.length('🐥') // 1 (not 2)
	string.length('é') // 1 (not sometimes 1 and sometimes 2)

Strings are stored in the database as UTF-8 strings, but you normally don’t need to know that when writing scripts. (Under the hood strings are Swift String types.)

When creating a string from binary data, the system figures out the character encoding automatically and creates a Unicode string value.

### Enumerations, Map, Filter, Visit, Sort

To enumerate the items in a collection, use `for item in collection` syntax — or visit, which takes a callback.

Arrays are enumerated in order. The order for tables is undefined.

Arrays and tables both support visit, map, filter, and sort.

array.map, array.filter, and array.sort return new arrays of values, and table.filter, table.sort, and table.map also return new tables.

The generating-links example, revised:

	def (urls)
		let links = array.map(urls), def (url)
			return '<a href=\(url)>\(url)</a>'
		return array.join(links, '')

### Numbers

There are two number types: integers and doubles.

When doing arithmetic, integers are automatically coerced to doubles when a double appears in the expression.

Integers are always 64-bit integers. (Ballard runs only on 64-bit systems, at least at this writing.)

### Error Handling

Error handling is via try/catch.

	try
		someScript()
	catch (error)
		msg(error.localizedDescription)

Errors are tables with `localizedDescription`, `domain`, and `code` objects. (The first two are strings, while `code` is an integer.) They may contain additional arbitrary objects.

Verbs for creating and throwing errors are `scriptError` functions.

To throw an error:

	var t = scriptError.new("Some error", "org.example.error", 42)
	t.arbitraryString = "Some extra data"
	scriptError.throwTable(t)

Or the short version, without additional data:

	scriptError.throw("Some error", "org.example.error", 42)

The domain and code parameters are both optional. The shortest version is just this:

	scriptError.throw("some error")
	
In that case, the domain is equal to the value at scriptError.domains.standard, and code is 0.

(See scriptError.domains and scriptError.errorCodes for domains and error codes you can use in your errors. You can make up your own, too, and it's typical that a given suite may have its own error domain.)

It’s worth noting that not all tables have to be stored in the database. Error tables live in memory, and disappear the moment there are no further references to the table. (Though you could, if you wanted to, copy an error table to the database.)

Note: though try takes an indented block of code, it does not define an inner scope. (`catch` does, however.) This is for the pragmatic reason that you might want to write something like this:

	try
		let feedTable = rss.parse(xmlString)
	catch (error)
		msg(error.localizedDescription)
	// Do things with feedTable

### Operators

Ballard has arithmetic operators, and these operators work on types besides just numbers:

	'foo' + 'bar' // evaluates to 'foobar'
	'foo' - 'o' // evaluates to 'fo' (removes one 'o' from the end)
	['foo', 'bar'] + 'baz' // evaluates to ['foo', 'bar', 'baz']
	['foo', 'bar'] - 'foo' // evaluates to ['bar']
	true + true // evaluates to true

These operators don’t work on *everything*, though. Binary data, scripts, outlines, and tables don’t support arithmetic operators.

There are also a number of built-in coercions. These are meant to be reasonable, so that you don’t end up with surprising results.

	8 + true // evaluates to 9
	true + 8 // evaluates to 9
	'foo' + 3 // evaluates to 'foo3'
	70 + 10.3 // evaluates to 80.3
	
The resulting type is the richer of the two types. An integer carries more information than a boolean, and a string carries more information than an integer, and a double carries more information than an integer.

Other operators include *, /, +=, -=, ++, and --.

### Additional operators

There are some additional operators beyond the standard set. They’re specified as English words.

	var x = 'I was swimmin’ in the Caribbean'
	x beginsWith 'I was' // true
	x endsWith 'bean' // true
	x contains 'swimmin' // true

Note: strings can have smart quotes inside — which is why `var x = 'I was swimmin’ in the Caribbean'` is okay. After *swimmin* is a right single (curly) quote.

	var x = [1, 2, 3]
	x beginsWith 1 // true
	x endsWith 3 // true
	x contains 2 // true
	x contains '2' // true, thanks to coercion

### Undefined variables

A variable can be undefined:

	var x

It has no type and no value. The `defined` built-in function can be used to test it: `defined(x)`. You can also compare it to nil, false, and 0:

	var x
	if x == nil
		msg('It’s nil.') // This runs.
	if !x
		msg('It’s false.') // This also runs.
	if x == 0
		msg('It’s zero.') // And this runs too.

Similarly, database objects may not exist: <code>defined(some.&#8203;table.&#8203;that.&#8203;doesnt.exist)</code> returns false.

There are cases where an undefined variable may be coerced to a value. Consider this:

	var x
	x++ // x now equals 1, because ++ implicitly converted it to an integer.

### Shadowed variables

This is a compiler error:

	var x = 10
	var x = "something else"

You can change the value of x, but you can’t re-declare it.

It’s also a compiler error when x is re-declared in an inner scope:

	var x = 10
	if test()
		var x = "Something else"

This is an error because it’s almost always a mistake on the part of the programmer — or is a poor choice, at best. Ballard solves the problem by making it impossible.

### Equality

Equality is always value-based. Even for objects passed by reference.

Simple example:

	var x = "A string"
	var y = "A string"
	if x == y
		msg("This line executes")

Tables:

	var x = (foo: 10, bar: "A string")
	var y = (bar: "A string", foo: 10)
	if x == y
		msg("This line executes")

The tables are equal because they have the same key/value pairs and their values are equal.

The following tables are *not* equal:

	var x = (foo: 10, bar: "A string")
	var y = (bar: "A string", foo: 10, baz: 3.141592)
	if x == y
		msg("This line never executes")

### Arrays

Like tables, arrays do not have to contain things of the same type. They often do — and it’s recommended that they do, because in general that’s a better programming practice. But the following is absolutely legal:

	var aTable = (foo: 10, bar: "A string")
	var anArray = (10, "some string", false, aTable)

Note that the literal syntax for tables and arrays is similar — they’re enclosed with ( and ) characters.

### Control flow

Ballard has conditionals, switch statements, and loops.

	if x != 19 || workspace.myScript(y) >= 100
		doSomething()
	else if x == 30.9
		doSomethingElse(x)
	else
		doYetOtherThing()
		
	switch(user.prefs.birthMonth)
		case 'January'
			msg('Cold!')
		case 'February'
			msg('Such a short month!')
		case 'March'
			msg('Best month to be born in.')
		default
			msg('Bully for you!')
	
	var i = 0
	loop
		i++
		if i >= 1000
			break
	
	while (expression)
		// do things
	
	for item in collection
		msg(nameof(item))
	
	var i
	for i = 0 to 999
		msg(i)
	
	for i = 999 downto 0
		msg(i)

### More about switch

The first case that evaluates to true ends the switch statement. A default case is not required.

	switch x
		case 7
			msg("x is 7")
		case true
			msg("This will execute whenever x is not 7 and is not 0 or false")

Coercions are automatically applied as necessary. In the above example, if x is 0, then neither case will be true.

Switch statements make the most sense when applied to value types. Though they can be used with tables, outlines, and scripts, it’s less common that it’s useful.
			
### Mime types

Strings and binary objects may include an extra piece of metadata, a mime type. This is especially useful when storing data in the database, since later on you might not remember that a binary object is, for instance, a PNG, or that a string is Markdown.

You can get and set the mimeType of any object like this:

	mimeType(s)
	setMimeType(@s, mimeType)

Note that setMimeType takes the address of an object rather than its value.

Note that this will only set a copy:

	var s = user.prefs.name
	setMimeType(@s, "text/plain")

That sets the mime type of the local variable s, which is a copy of user.prefs.name. To set the mime type of user.prefs.name:

	setMimeType(@user.prefs.name, "text/plain")

For any object that isn’t a string or binary data, these calls result in a runtime error.

### Addresses

A variable can contain the address of an object.

	def changeStringValueToFoo(adrItem)
		adrItem^ = "Foo"
	var adrName = @user.prefs.name
	changeStringValueToFoo(adrName)

In this case, adrName is the *address* of user.prefs.name rather than a copy of its value. `changeStringValueToFoo` dereferences the passed-in address in order to change the value at user.prefs.name.

(The `adr` prefix is a convention for variables that contain addresses. That prefix isn’t part of the language syntax.)

Note that addresses are not used all that often, since tables are already passed by reference. (If they weren’t, you’d be passing their addresses around all the time, which makes for messy syntax.)

But one case where you will always use addresses is with `setMimeType`.

Here’s how you’d set the mime type of every object that's a string in a given table:

<pre>def setMimeTypeForObjectsInTable&#8203;(someTable, type)
	def callback(adrItem)
		if typeof(adrItem^) == stringType
			setMimeType(adrItem, type)
	table.visitAddresses&#8203;(someTable, callback)</pre>

`table.visitAddresses` differs from `table.visit` in that it calls the callback with the address of each item in a table.

The callback doesn’t take a `key` parameter, because you can get an object’s key using `nameof`:

	let adrItem = @user.prefs.birthMonth
	msg(nameof(adrItem^)) // displays "birthMonth"

Note how this is different for non-addresses:

	let s = user.prefs.birthMonth
	msg(nameof(s)) // displays "s"

### Expressions in key paths

Any part of a key path (whether used in an address or not) can be an expression.

	let appName = "MyCoolApp"
	let t = user.prefs.[appName].isFirstRun

In this case, t gets the value at user.prefs.MyCoolApp.isFirstRun.

This is also useful when a key contains a . or space or other character not normally allowed as part of a key path. In general it’s best to avoid this, but you can do the following

	var t = user.prefs.["My.Cool.App Which is Cool"].isFirstRun

In this case `My.Cool.App Which is Cool` is the key. Even though it contains dots and spaces, it’s still legal. It’s just awkward to work with.

### Standard Library

Ballard’s standard library is built-in to the language. A hello-world program uses the builtin `msg` verb:

	msg('Hello, world!')

(Note: a function designed to be called from other scripts is often called a “verb.”)

msg is defined as printing text to whatever is the defined place to print text to. In $APPNAME that’s in the status bar of the frontmost window. In other places it might be a console pane or window (for instance).

Other top-level verbs include count, nameof, typeof, mimeType, and setMimeType.

Other verbs are grouped in system tables. Some of those verbs are implemented in the kernel; some are implemented as scripts. You can view the source of those that are implemented as scripts (the scripts appear in the database).

Some categories are named for the various types: date, string, and data verbs. Other groups: xml, json, tcp, and so on. In some cases there are subtables: tcp.dns, for instance.

Some examples:

	string.mid(s, start, length)
	tcp.dns.dottedID(host)
	rss.parse(xml)
	json.parse(s)
	download(url, method, headers, options) // Headers and options are tables
	plist.write(item, f)
	outline.withOPML(s)
	file.writeWholeFile(f, d)
	markdown.toHTML(s)
	
### Creating an object

As previously noted, objects can be created via assignment:

	user.prefs.favoriteFood = 'spaghetti'

Another method — useful for tables, outlines, and scripts, especially — is via the various `new` functions.

	workspace.movieListings = table.new()
	workspace.stressTestTheServer = script.new()

Tables can also be created with a literal syntax:

	workspace.movieListings = ("foo" : 8, "bar" : "Some string")
	var t = (x : someValue) // x should be a string: its value is the key

### Suites

$APPNAME’s standard library can be extended with suites. Suites can be libraries, collections of related functions, or even mini-apps. They are automatically installed in the suites table.

When looking up a symbol, the suites table is checked after the system tables.

Imagine you wrote a set of scripts that implement the client side of a web app’s API. Let’s say you were writing scripts that implement Twitter’s API.

You’d create a suite named twitter. Scripts in the top level of the suite would be available to other scripts:

	let timeline = twitter.downloadTimeline()

A suite might connect to a web app, scriptable Mac app, command-line tool, separate database — or it might be completely internal to $APPNAME.

(In the file system, suites are stored as separate databases, which makes them easy to install and uninstall. However, $APPNAME provides the illusion that it’s all one single database. Frontier users will recognize that $APPNAME suites are a combination of Frontier suites and Frontier guest databases.)

Suites can declare dependencies: a top-level table named dependencies list the names, URLs, and versions of other suites that are required.

### User Interface

$APPNAME will provide a web server and embedded WebKit view — you can write web apps using Ballard. (You can also run those web apps in an external browser.)

Ballard can also run xibs — you can create windows and views in Xcode that Ballard can display and run.

### Website framework

Ballard includes a suite for generating web pages and entire sites based on templates, assets, and scripts. They can be generated as static pages (which of course could include JavaScript, or be PHP files, or whatever — they don’t have to be entirely static, though the output is files-on-disk).

The framework for serving dynamic web apps will also use the website framework.

(Nothing I’ve ever seen has come close to the power and flexibility of Frontier’s website framework. The goal is to make Ballard’s website framework similarly powerful.)

(Yes, I’ll be switching my blog over to $APPNAME.)

### Scripting Mac Apps

TBD

### Threading

$APPNAME executes scripts outside the main thread. The main thread is reserved for the application.

There are no functions that are asynchronous that return by calling a block. It’s not like Node.js, for instance. Instead, a call to `download` blocks until it’s finished.

We think this is a simpler model, particularly for newer programmers. Do this, then do the next line, then the next line, and so on.

$APPNAME doesn’t have verbs for directly creating threads, but it does have queues. There is a global queue, and scripts can create their own queues.

This does mean that scripts may be running on multiple threads.

(Note about the implementation: Ballard’s compiler and evaluator are both thread-safe. It does not use a single-threaded parser; it does not have a global interpreter lock. Different threads are true different machine threads.)

### Locking

You can lock a block of code:

	lock {
		// critical section here
	}

`lock` is not recursive.

You can also lock a section of the database:

	table.lock(workspace) {
		// No other scripts can read, write, or execute anything in the workspace table (or subtables).
		// It doesn’t matter if the other scripts called table.lock or not.
	}

`table.lock` *is* recursive.

The reason for using blocks: we don’t want to have to remember to call `unlock` or `table.unlock`, since that would be a source of errors. (Unlock functions don’t exist.)

Ideally locks are rarely needed. But this *is* a multi-threaded environment with a shared database. The time spent inside a lock should be as minimal as possible.

(Implementation note: locks are implemented via NSLock, rather than via @synchronized, which is slow and doesn’t allow for non-recursive locking, or via spinlocks, which assume infrequent contention.)

### Eval

There is no `eval` function, since it’s evil.

### Debugging

When running in $APPNAME, you can debug Ballard scripts using the same pause, continue, step-into, -over, and -out that you’re used to from other debuggers. You can set breakpoints.

You can view the entire stack as a set of tables, and change the values in the stack while debugging.

### Memory

Ballard is not garbage-collected.

It’s built with Swift, Cocoa, and ARC — and the lifetime of Ballard objects is managed the same way any other Swift objects are managed with ARC. (Since Ballard objects are Swift objects.)

### Short-term persistence

In addition to local variables and the database, there is a temporary table, which can contain subtables (of course), and which lives only for the duration of the app’s run.

	temp.foo = 'This will disappear when the app quits.'

The `temp` table is stored in memory. (It’s called “temp” instead of “tmp” because “temp” is more obvious to new scripters.)

### Performance

It will never be as fast as Swift, but performance is expected to be very good. Standard library functions are Swift methods. The collection types are Swift Array and Dictionary objects.

(I’ll revise this section with numbers once I know what performance is *actually* like.)

### Profiling

There will be a profiler. TBD.

### Embedding

The primary use of Ballard is as $APPNAME’s scripting language. However, it is designed to be embeddable, with or without the object database. (The standard library is included even without the object database.)

When embedded in another app, if the object database is not included, then looking up dotted identifiers (`user.prefs.foo`, etc.) is the responsibility of the app.

The embedding app is free to add to the standard library. For instance, say you embedded $APPNAME in a text editor — you’d want to give scripts access to windows and text objects, and you’d want to provide functions for manipulating text.

You might provide a virtual table. Here’s how a script might make lower-case all the text in the frontmost window:

	var w = TextEditor.frontWindow()
	w.text = string.lowerCase(w.text)

(Note: I plan to embed Ballard in at least one app besides $APPNAME. It’s important to me that this works well. And I plan to provide the source to a sample app.)

One possible benefit of embedding: you could write a bunch of your app’s functionality in scripts, and then have those scripts update over-the-air, rather than requiring a new entire-app download when you make changes. (This may not be possible with sandboxed apps or Mac App Store apps, of course. But neither $APPNAME nor the other app I’m working on will be sandboxed or on the MAS, so I don’t care.) We did this over-the-air updating 15 years ago with Frontier. It makes updating an app more like updating a web site, which is cool.

### iOS and other platforms

Ballard is designed for use in $APPNAME, a Mac app, and in other Mac apps. However, there are no technical reasons why it couldn’t be embedded in iOS apps.

(Since Swift is open source, it should be possible to port to Windows and Linux. I have no plans for any such ports. However, I’ll strongly consider changes needed for iOS, though I have no plans to create $APPNAME for iOS or to use Ballard in any iOS apps.)

### Where the name comes from

Ballard, where the author lives, is a [neighborhood by the water in northwest Seattle](http://en.wikipedia.org/wiki/Ballard,_Seattle).

### Sample scripts

This is a scratchpad where I’m working out stuff. It may end up as bonus material for this document, or it might get deleted.

#### RSS parsing

	def downloadAndParseFeed(url)
		let httpResult = download(url)
		return rss.parse(httpResult.body)
	
<pre>let feedTable = downloadAndParseFeed&#8203;('http://inessential.com/&#8203;xml/rss.xml')
msg(feedTable.title)
array.visit(feedTable.items, def (oneItem))
msg(oneItem.description)</pre>
	
	def linkForItem(item)
		if item.permalink
			return item.permalink
		return item.link
	let links = array.map(feedTable.items, linkForItem)
		
#### JSON parsing
	
	def downloadAndParseJSON(url)
		let httpResult = download(url)
		return json.parse(httpResult.body)
		
<code>let parsedJSON = downloadAndParseJSON&#8203;("https://example.org/&#8203;jsonEndpoint")</code>
	
	// transform JSON	
	def transformJSON(parsedJSON)
		return table.map(parsedJSON, def(oneItem))
			return [name: oneItem.title, uniqueID: oneItem.id]	
	
	let JSONAsTable = transformJSON(parsedJSON)
	
	// store in scratchpad and display
	scratchpad.JSONObjects = JSONAsTable
	edit(@scratchpad.JSONObjects)
	
#### Plists

	var t = plist.read("~/Desktop/some.plist")
	var extraInfo = table.new()
	extraInfo.foo = 1234
	extraInfo.bar = "Some string"
	t.addedStuff = extraInfo
	plist.write(t, @"~/Desktop/transformed.plist")
	
#### Errors

<pre>def parseRSSFile(f)
	if !file.exists(f)
		var errorTable = scriptError.new('The file \(f) was not found.', scriptError.domains.&#8203;file, scriptError.&#8203;errorCodes.fileNotFound)
		errorTable.filePath = f
		scriptError.&#8203;throwTable&#8203;(errorTable)
	return rss.parse&#8203;(file.readWholeFile(f))</pre>
	
<pre>try
	let feedTable = parseRSSFile("~/Desktop/rss.xml")
catch (error)
	if (error.code == scriptError.errorCodes.fileNotFound && error.domain == scriptError.domains.file && error.filePath)
		dialog.alert("Couldn’t parse RSS feed because the file \(error.filePath) wasn’t found.")
	else
		dialog.alert&#8203;(scriptError.localizedDescription)
	return
msg('There are \(count(feedTable.items)) in the feed.')</pre>
	
#### Keychain

<pre>let password = keychain.&#8203;passwordForAccount&#8203;('SomeService', 'myusername')
if !password
	msg('Couldn’t find a password.')
else if count(password) < 8
	msg('That’s a pretty short password.')
else
	msg('Seems like a good password. At least it’s 8 or more characters.')</pre>
		
<pre>keychain.deletePassword&#8203;('SomeService', 'myusername')
msg('Deleted the password anyway.')</pre>
	
<pre>keychain.savePassword&#8203;('SomeService', 'myusername', 'abc123')
msg('Saved a really bad password for you.')</pre>
	
<pre>let webPassword = keychain.&#8203;passwordForURL&#8203;('https://some.paywall.com/')
if !webPassword
	msg('Yeah, I don’t have an account either.')</pre>

#### Basic app scripting

	let t = app.frontmost()
	app.quit(t)
	
	app.launch('Napkin')
	app.bringToFront('Napkin')

	def quitAppCallback(oneApp)
		if oneApp != '$APPNAME'
			app.quit(oneApp)
	array.visit(mac.runningApps(), quitAppCallback)

	app.hide('$APPNAME')

<pre>webBrowser.openURL&#8203;('http://daringfireball.&#8203;net/')</pre>
	
#### Basic outline scripting

	def topLevelStringsInOutline(outline)
		var topLevelStrings = []
		op.visit(outline, def(s, indentLevel, hasChildren, id))
			if indentLevel < 1
				topLevelStrings += s
		return topLevelStrings
	
	def numberedItemsInArray(anArray)
		var i = 0
		return array.map(anArray, def(oneString))
				i++
				return "\(i). \(oneString)"
	
<pre>let topLevelStrings = topLevelStringsInOutline&#8203;(workspace.notepad)
return numberedItemsInArray&#8203;(topLevelStrings)</pre>
	
#### Shell

	def hgStatusForDirectory(folderPath)
		shell.runCommandWithArray(['pushd', folderPath])
		let result = shell.runCommand('hg status')
		shell.runCommand('popd')
		if result.stderr
			scriptError.throw(result.stderr)
		return result.stdout

#### File

<pre>let f = "~/Desktop/sub/folders/&#8203;are/cool/file"
file.sureFilePath(f)
file.create(f)
file.rename(f, "newName")
msg(file.creationDate(f))</pre>

#### Date

<pre>let d1 = date.new('Mon, 04 May 2015 11:31:49 -0700') // Understands RFC 822 date strings
let d2 = date.new('2015-04-23T04:26:20Z') // Understands RFC 3339 date strings
let d3 = date.new() // Current date
var dateComponents = date.components(d3)
msg(dateComponents.year)
dateComponents.year++
let d4 = date.withComponents&#8203;(dateComponents)</pre>
	