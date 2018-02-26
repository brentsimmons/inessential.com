@title Mobile Services and Blob Storage
@pubDate 2014-04-22 11:24:41 -0700
@modDate 2014-04-22 11:32:18 -0700
This is a quick write-up of how I got this working.

Here’s the situation:

* I want to store images and other binaries in Azure blob storage (which is like Amazon S3) rather than in a SQL database or NoSQL table.

* I want the client to upload directly to blob storage — I don’t want the image data to pass through the API server.

I struggled with this. For a while I was looking at the REST API and building a SharedKey. It wasn’t until I found [Chris Risner’s page on this from last year](http://chrisrisner.com/iOS-and-Mobile-Services-and-Windows-Azure-Storage) that I found what I needed. (Thanks tons to Chris for writing this up.)

So this tutorial exists in case you’re in the same boat.

I’ll assume you already have a Mobile Service and know how to set up custom APIs. I’ll talk about the server side mostly, since you already know how to use NSURLSession and friends.

#### Get a blobService

Set up a storage service if you haven’t already. (New > Data Services > Storage.) A storage service is NoSQL table storage, queues, and blobs.

Add the storage service’s name and primary access key to your Mobile Service’s key storage (see the Configure pane, under app settings). Key names such as BLOB\_ACCOUNT and BLOB\_ACCESS\_KEY are fine. Whatever you want. 

In your code:

<code>var azure = require('azure');</code>

The azure module is available without you having to do anything. Just require it to use it.

The azure module gets you a blobService:

<code>var blobService = azure.&#8203;createBlobService&#8203;(accountName, key, host);</code>

accountName and key should come from your Mobile Service’s key storage — <code>request.&#8203;service.&#8203;config.&#8203;appSettings.&#8203;BLOB_ACCOUNT</code>, for instance.

The host is <code>accountName + '.blob.core.windows.net'</code>.

Whenever you’re going to do something with blob storage, get a blobService.

#### Creating a container

<code>blobService.&#8203;createContainerIfNotExists&#8203;(containerName, function(err)…</code>

This creates a private container. (You can create public containers too, but that’s outside of the scope here. It’s easy, though.)

#### Listing files

<code>blobService.&#8203;listBlobs&#8203;(containerName, function(err, results)…</code>

The results are in JSON. You could return those to the client, or filter them to just filenames or whatever the client needs.

#### Deleting a file

<code>blobService.&#8203;deleteBlob&#8203;(containerName, filename, function(err)…</code>

#### Uploading

Here’s the fun part. You don’t want the image binary to go through the API server. Instead, the API server generates a temporary shared access URL that will allow the client to upload directly.

First use createContainerIfNotExists. (I assume you have some way of deciding what the container names should be. They could be based on a person’s user ID, for instance. Depending on the security needs of your app, it may be a good idea to hash the container names, so they’re not personally identifiable.)

You need a sharedAccessPolicy.

<code>var sharedAccessPolicy = {</code><br />
<code>&nbsp;&nbsp;AccessPolicy: {</code><br />
<code>&nbsp;&nbsp;&nbsp;&nbsp;Permissions: 'w',</code><br />
<code>&nbsp;&nbsp;&nbsp;&nbsp;Expiry: azure.date.&#8203;minutesFromNow(5)</code><br />
<code>&nbsp;&nbsp;}</code><br />
<code>}</code>

Then you generate the URL to return to the client:

<code>var sasURL = blobService.&#8203;generateSharedAccessSignature&#8203;(containerName, filename, sharedAccessPolicy);</code><br />
<code>var accountName = request.&#8203;service.&#8203;config.&#8203;appSettings.&#8203;BLOB_ACCOUNT;</code><br />
<code>var urlForUploading = 'https://' + accountName + '.blob.core.windows.net' + sasURL.path + '?' + qs.stringify(sasURL.queryString);</code><br />

(Somewhere above this you need <code>var qs = require('querystring')</code>.)

Return this URL to the client.

The client can use an <code>NSURLSession&#8203;UploadTask</code>. Use the PUT verb. Add Content-Type and Content-Length headers. (It’s a good idea to add Content-MD5 too, but not required.)

#### Downloading

It’s almost exactly the same as uploading, except that sharedAccessPolicy&#8203;.AccessPolicy.&#8203;Permissions is 'r' instead of 'w'.

I have the server respond with a redirect to the URL.

That’s it. Pretty easy.
