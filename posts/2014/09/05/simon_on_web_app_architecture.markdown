@title Simon on Web App Architecture
@pubDate 2014-09-05 10:17:43 -0700
@modDate 2014-09-05 10:17:43 -0700
<a href="http://iamsim.me/web-app-architecture-discussion/">Simon Ljungberg writes</a>:

>We are currently dealing with some of this on Bloglovin because our web app is starting to get split up between a few different services. We’re tackling this by building a collection of components. These components represent different UI elements (kind of like Boostrap I guess). Each service includes the library of components as a dependency, and as such we update the code in one place and the dependency in the other places.

My <a href="http://inessential.com/2014/09/04/web_app_architecture_question">previous post</a> could be summed up as just this question: “Should I use one Rails app or a collection of Node/Sinatra/whatever apps?”

Almost everybody says to use a collection of apps rather than a monolithic app. Which is cool, because that’s what I’d rather do.
