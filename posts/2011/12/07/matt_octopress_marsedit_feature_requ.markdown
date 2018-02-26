@title Matt + Octopress + MarsEdit feature request
@link http://mattgemmell.com/2011/09/12/blogging-with-octopress/
@pubDate Wed Dec 07 11:04:11 -0800 2011
@modDate Wed Dec 07 11:04:11 -0800 2011
Matt Gemmell is <a href="http://mattgemmell.com/2011/09/12/blogging-with-octopress/">Blogging With Octopress</a>. I think that’s cool. (Yes, that article is a few months old.)

This site is run by <a href="http://inessential.com/2009/01/30/new_publishing_system_tour_of_my_head">my own custom software</a>, but the idea is the same: <a href="http://daringfireball.net/projects/markdown/">Markdown</a> files are stored in a directory structure on disk, and a Ruby script generates the weblog and rsyncs it to the server.

I *love* blogging this way. I still get to use <a href="http://www.red-sweater.com/marsedit/">MarsEdit</a>, even.

I can use MarsEdit because I run a local webserver that has a Ruby CGI I wrote that implements the <a href="http://xmlrpc.scripting.com/metaWeblogApi.html">MetaWeblog XML-RPC API</a>.

But I wonder if it would make sense for MarsEdit to handle this situation natively: that is, it could read and write files directly on disk. The directory structure is simple, with relative paths like 2011/04/16/some_file.markdown.

If MarsEdit worked that way, then it would allow developers to write blog-generation software like mine and like Octopress, and still have MarsEdit support without having to jump through the hoops of running a local webserver and a CGI script.
