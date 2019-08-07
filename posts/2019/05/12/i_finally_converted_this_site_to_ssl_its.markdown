@pubDate 2019-05-12 22:10:05 -0700
@modDate 2019-05-12 22:10:05 -0700
I finally converted this site to SSL. It’s not the first site I’ve converted, but it’s the last.

It wasn’t hard. I’m using [Let’s Encrypt](https://letsencrypt.org/), and my hosting provider handles all the details, including renewing and updating.

The one thing I had to do manually was edit the .htaccess file so that http requests get redirected to https.

I’m still dubious on the use of https for sites like this one — but mainly I worry about sites that are hard to convert or where there’s nobody to do the work. What happens to what remains of the web’s history if, at some point, browsers won’t let us visit those sites anymore?

I’m thinking specifically of [alexking.org](http://alexking.org/), [penmachine.com](http://www.penmachine.com/), and [aaronsw.com](http://www.aaronsw.com/). There are plenty of others.

<p style="text-align:center">* * *</p>

The change from http to https means all the permalink and guids changed in my feed — so you may get reruns in your RSS reader. Sorry about that!
