@title Swift Bikeshed Week Three: LangValue

(Note: this is a data modeling and error-handling exercise. No tricky algorithms are needed.)

Pretend you’re writing the runtime for a language.

It’s a simple language with just three data types: integer, string, and table.

Your mean, meddling, micro-managing boss told you to use a single thing to represent values in this language, and that thing has to be named LangValue.

Your mean boss — who hates classes and Objective-C — also said she wants to see *two* solutions. Here are your choices:

* LangValue as an enum.
* LangValue as a struct.
* LangValue as a protocol, with structs named LangValueInt, LangValueString, and LangValueTable that implement LangValue.
* LangValue as a protocol, with extensions to the built-in Swift data types Int, String, and Dictionary that make them implement LangValue.

Pick any two.

## Spec

- Integer and string values are immutable.
- Table values are *not* immutable. Table keys must always be Swift strings. Tables may contain other tables.
- A LangValue can never change its type.

The API for creation must be something like this, though not necessarily exactly like this (could be one or more init methods instead, for instance):

	LangValueWithInteger(n: Int) -> LangValue
	LangValueWithString(s: String) -> LangValue
	LangValueTable() -> LangValue //empty table

LangValue API must be conceptually like this:

	type (readonly) -> LangValueType.Integer, .String, or .Table

The following throw `LangCoercionError` for tables:

	integerValue (readonly) throws -> Int
	stringValue (readonly) throws -> String
	valueByAddingValue(LangValue: value) throws -> LangValue

A String can be coerced to an Integer via whatever built-in coercion Swift (or NSString) provides. Don't sweat this. It's okay if it returns 0 in cases like "some string".

When a String and an Integer are being added, the Integer is coerced to a String, and the result is LangValueType.String. `123 + "123" == "123123"`

(In other words: though Strings can be coerced to Integers, Integers are coerced to Strings when doing automatic coercion.)

The following throw `LangCoercionError` when the receiver isn't a table.

	setObjectForKey(object: LangValue, key: String) throws
	removeObjectForKey(key: String) throws
	objectForKey(key: String) throws -> LangValue?
	keys() throws -> [String]

## Tests

### Adding values

This code (or the equivalent) must work:

	let s = LangValueWithString("This is a string")
	let n = LangValueWithInteger(42)
	let someValues = [s, n]

	func addIntegerValuesInArray(values: [LangValue]) -> LangValue {

		// Return LangValueType.Integer object
		...write code here
	}

	func addStringValuesInArray(values: [LangValue]) -> LangValue {

		// Return LangValueType.String object
		...write code here
		}
	
	let intResult = addIntegerValuesInArray(someValues)
	assert(intResult.integerValue() == 42)

	let stringResult = addStringValuesInArray(someValues)
	assert(stringResult.stringValue() == "This is a string42"

	let unknownResult = s.valueByAddingValue(n)
	assert(unknownResult.type == .String)

### Tables and Sets

This code (or the equivalent) must also work:

	let t = LangValueTable()
	t.setObjectForKey(LangValueWithInteger(10), "SomeInt")
	let someString = LangValueWithString("Some string")
	t.setObjectForKey(someString, "SomeString")

	let subtable = LangValueTable()
	subtable.setObjectForKey(LangValueWithInteger(50), "SubtableInt")
	let anotherString = LangValueWithString("Another string")
	subtable.setObjectForKey(anotherString, "SubtableString")
	t.setObjectForKey(subtable, "Subtable")

	func recursiveSetOfStringsInTable(table: LangValue) -> Set<LangValue> {
		// Get all LangValueType.String objects from a table and its subtables and return them as a Swift set.
		...write code here
	}

	let setOfStrings = recursiveSetOfStringsInTable(t)
	assert(setOfStrings == Set([someString, anotherString])

Note: The code in both tests probably needs error handling.