@title Init Question
@pubDate 2015-03-01 13:00:57 -0800
@modDate 2015-03-01 13:21:44 -0800
What’s the best practice for this situation?

Let’s say you have an object where initWithSomething could fail due to bad inputs or other error.

Let’s also say that, if it fails, an error should probably be presented to the user.

If it helps to think about a concrete case, think of a Core Data stack object. (*This post is not about Core Data*. This is just an example.)

Init might look something like this:

<code>- (instancetype)&#8203;initWithFolder:&#8203;(NSString \*)&#8203;folder modelName:&#8203;(NSString \*)&#8203;modelName databaseName:&#8203;(NSString \*)&#8203;databaseName;</code>

There are two reasons it could fail:

1. Inputs are bad. (For instance: folder is nil, or modelName has a typo.)

2. A method called during init fails. For example, <code>-[NSPersistentStoreCoordinator addPersistenStoreWithType:&#8203;configuration:&#8203;URL:&#8203;options:&#8203;error:]</code> could fail.

I can think of a few options, and I’m not sure I like any of them. So I’d love to know what you think.

#### Option 1: in-out error parameter

I don’t think I’ve ever seen a failable initializer with an in-out NSError ** parameter. (Do they exist? Maybe they do and I just haven’t noticed.)

The init method would look like this:

<code>- (instancetype)&#8203;initWithFolder:&#8203;(NSString \*)&#8203;folder modelName:&#8203;(NSString \*)&#8203;modelName databaseName:&#8203;(NSString \*)&#8203;databaseName error:&#8203;(NSError **)error;</code>

That seems ugly and unconventional to me. But it would reflect reality pretty well.

<i>Update 1:15 pm:</i> This is the winner! Look at NSString.h to see some examples.

#### Option 2: error property

Don’t fail in the initializer. Instead, create a property for the error:

<code>@property (nonatomic) NSError *initError;</code>

The caller of initWith… would have to check <code>initError</code> right after to see if there was an error. Ugly and unconventional again.

#### Option 3: initialize lazily

The main reason for this object is to provide properties for other objects and hide how they’re created.

The example could have a property like this:

<code>@property (nonatomic) NSManagedObjectContext *context;</code>

All the initialization of the stack could be put off until <code>context</code> is first referenced.

But, then, there’s still the issue of what to do with errors. Something like this instead of a property?

<code>- (NSManagedObjectContext \*)context:(NSError **)error;</code>

Ugh. Weird.

But maybe it’s less weird if the API is something like this:

<code>@property (nonatomic) NSManagedObjectContext \*context;</code><br />
<code>- (BOOL)setupManagedObjectContext:(NSError **)error;</code>

The caller of initWith… will have to call <code>setupManaged&#8203;Object&#8203;Context</code> before referencing the <code>context</code> property.

This is also weird because setting up <code>context</code> should be completely in the hands of the Core Data stack object. It shouldn’t be something a caller has to remember to do.

#### Option 4: assertions and faith

Use <code>NSParameterAssert</code> and <code>NSAssert</code> to catch programmer errors in debug builds — then assume that, once programmer errors are fixed, nothing else that technically can fail will actually fail.

This would mean believing that, in this case, <code>-[NSPersistentStoreCoordinator addPersistenStoreWithType:&#8203;configuration:&#8203;URL:&#8203;options:&#8203;error:]</code> would never fail as long as the inputs were good.

Arguably you should just call <code>abort()</code> if such a method fails with good inputs, on the grounds that the device has probably caught fire.

But still, that requires a certain amount of optimism — but optimism means doubt, and our job as programmers is to remove doubt.

#### Option 5: don’t use a separate object for this

Give up on the idea of encapsulating all this in reusable code. Instead, have the app delegate (or similar high-level object) do the setup. Presumably that high-level object can show errors to the user and decide what to do if things go wrong.

This answer is a bummer, though. I like reusable objects and I don’t like copy-and-paste.

But maybe I’ve proven that this option is the only responsible choice.

What am I missing?
