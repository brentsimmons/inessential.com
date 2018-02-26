@title Santiago on Web Apps
@pubDate 2014-09-05 11:00:59 -0700
@modDate 2014-09-05 11:00:59 -0700
<a href="http://blog.svpino.com/2014/09/04/my-two-cents-about-some-web-app-architecture-questions">Santiago Valdarrama writes</a>:

>All the logic in my API would be packaged as a standalone library and the REST interface will simply expose this logic. I can import and use the library directly in my code, and my applications will talk to the methods in the library without having to go through HTTP. These methods contain 100% of the logic so I won’t be duplicating code neither incurring in unnecessary latency.

If I understand correctly, then this means that my several different Node/Sinatra/whatever apps would each have their own copy of this library. I hadn’t thought about that approach, and I’m a little worried about how I’d manage making sure it’s up-to-date in each place. But that kind of thing (via Ruby gems, npm, Git, Mercurial, etc.) is supposed to be easy these days.

The approach I imagined is that an API server would play that role, and the various apps would talk to the API server via http to do the common things. (And the in-browser app would talk to that API server too.)

I hadn’t thought of Santiago’s approach. Definitely worth considering.
