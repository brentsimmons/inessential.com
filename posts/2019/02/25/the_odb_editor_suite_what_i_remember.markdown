@title The ODB Editor Suite: What I Remember
@pubDate 2019-02-25 15:15:23 -0800
@modDate 2019-02-25 15:15:23 -0800
The ODB Editor suite — which came up on the latest [The Talk Show podcast](https://daringfireball.net/thetalkshow/2019/02/22/ep-244) — happens to be something I know about.

Here’s what I remember about how it happened… ([Dave Winer](http://scripting.com/) or [Rich Siegel](https://twitter.com/siegel) may remember more, or better, and may correct me, and maybe not.)

I was working at UserLand, or maybe still doing contracting, or maybe I was still just an enthusiastic member of the community. I forget. But I was nearby when this happened.

Dave had written a website rendering framework for UserLand Frontier that generated static sites. This was the mid-to-late 1990s. The pages were stored in Frontier’s object database, which had its own text editor.

The problem was that some people wanted to use [BBEdit](https://www.barebones.com/products/bbedit/) instead of Frontier’s built-in text editor, because, well BBEdit was (and still is) awesome.

So we wanted to make it so you could be looking at text in Frontier, and then choose a menu command to open it in BBEdit for editing — and then *have it automatically update in Frontier’s object database when you close it in BBEdit.*

In other words, we wanted BBEdit to be an external editor for Frontier’s object database.

So Dave — working with Rich? Doug Baron? Jim Correia? I honestly don’t know who all worked on the details, though it wasn’t me — came up with the ODB Editor suite, which any text editor could support. (The BBEdit site has [documentation](https://www.barebones.com/support/develop/odbsuite.html).) BBEdit supported it, and other text editors added support too over the years.

The ODB part stands for Object Database.

Years later, for [MarsEdit](https://www.red-sweater.com/marsedit/) 1.0 (or some early version), I implemented the server side of the ODB Editor suite, so you could open something in MarsEdit in BBEdit, and have it save back to MarsEdit.

PS I use MarsEdit to this day. MarsEdit and BBEdit still support the ODB Editor Suite. Just to try it out, I’m writing this post in BBEdit, and it automatically updates the text in MarsEdit. It still works. :)
