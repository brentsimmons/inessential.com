@title SwiftUI Is Still the Future
@pubDate 2019-10-21 13:20:15 -0700
@modDate 2019-10-21 13:24:45 -0700
We’ve been using SwiftUI in NetNewsWire for iOS, for its settings screen and related pieces (such as adding an account).

But now we’re redoing that code in classic UIKit. [Maurice Parker](https://github.com/vincode-io), NetNewsWire for iOS lead developer, lists the limitations we ran into with SwiftUI:

>1) Unable to customize cell selection color for our vibrant cell selection requirement.  I was able to hack around it, but it made cells behave strangely.  You couldn’t tap and hold the cell.  You also couldn’t scroll using the modified cells.
>
>2) No pop back to root for NavigationView.  Longer scene flows weren’t possible.
>
>3) ActionSheet flat out just crashes if you use it on an iPad app. [https://forums.developer.apple.com/thread/124530](https://forums.developer.apple.com/thread/124530)
>
>4) TextField will crash the app if it has the cursor and is hidden.  We wanted this for the show/hide password functionality.
>
>5) There is no way to display attributed text.  You have to bridge to UIKit and use a UITextField that has a modified intrinsicContentSize calculation.  We had to take input from GeometryReader and pass it into the UITextField to calculate intrinsicContentSize.
>
>There are more, some of which I have probably forgotten about.

We very much want to use SwiftUI, and we believe it’s the future of Mac and iOS development — but emphasis should be on *future*, because it’s not quite ready in the present.

Which should surprise nobody, given that it’s so new. But I thought it might be interesting to know exactly what issues we ran into when using it.

We look forward to the day when we can use it everywhere, but we suspect it will be incremental. Hopefully next year we’ll be able to do the Settings screen using SwiftUI. And maybe some parts of the Mac app, too.

PS Once we’re ready for a public beta of NetNewsWire for iOS, we’ll announce it here and on the [NetNewsWire blog](https://nnw.ranchero.com/), and you’ll be able to sign up to get it via TestFlight.
