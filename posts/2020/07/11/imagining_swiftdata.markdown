@title Imagining SwiftData
@pubDate 2020-07-11 14:29:37 -0700
@modDate 2020-07-11 14:29:37 -0700
If SwiftUI and Combine are the new, Swifty V and C in MVC, where’s the M?

I keep thinking that Core Data, amazing as it’s been, is part of NeXT-world Apple, and we’re due for a Swift data model framework.

Instead of defining your model in a schema editor (a la Core Data), you’d use a Swift DSL — which would be nice because you wouldn’t have to keep the schema and your model code in sync. It would be just one thing.

It would use (or at least allow for) value types over reference types. It would use protocols instead of inheritance. It would play perfectly well with Combine.

It might not even use SQLite — I can imagine Apple creating a storage system more purpose-built. It might be built with syncing in mind *first* rather than as afterthought.

I have no inside knowledge. And maybe this is just wishful thinking. But it surely seems to me that something like the above should be coming — it would be weird if not, I think. Maybe next year?
