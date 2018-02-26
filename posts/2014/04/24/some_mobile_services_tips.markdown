@title Some Mobile Services Tips
@pubDate 2014-04-24 11:36:18 -0700
@modDate 2014-04-24 11:36:18 -0700
Here are a few tips, in no particular order, on using Mobile Services. I have months of experience, but not years, so treat as such.

#### Custom APIs Only

I don’t use the scripts attached to the tables. Instead I create all custom APIs. This lets me define exactly what callers can do.

#### Create SQL Tables Using Command Line

If you create a table using the portal, you get an id column that’s a string, plus some extra columns that you don’t need if you’re using custom APIs only.

Make sure you have the azure command line tool installed. (It’s a Node package.) Do <code>azure mobile table create --help</code> to see your options.

Note the <code>--integerId</code> flag — that’s what you want. If you use that flag when creating a table, you get a table where the id column is a bigint, and no extra columns.

#### Database queries and updates

It’s pretty easy to use table.where, table.insert, table.update — but I use request.service.mssql.query for almost everything, for reasons of efficiency and control.

#### Advanced Database Admin

If you have to do more than the portal will let you, use the [Azure SQL Server command line](http://inessential.com/2014/04/21/azure_sql_server_command_line).

Hopefully you won’t need to — but it’s not scary. (It’s much like using the sqlite3 command line.)

#### You May not Need the iOS Framework

If you’re using Facebook or Twitter authentication, you need the framework.

But since we’re not, we don’t. Here’s the thing: connecting to the service is really easy without the framework.

You call your methods as you’d think, with URLs like https://yourappname.azure-mobile.net/custom/api — and you need to do just two extra things:

1. Add an x-zumo-application header with the app’s public access key.

2. For authenticated calls, add an x-zumo-auth header with the JWT that Mobile Services returns.

After that it works like any other REST + JSON interface.

#### Create Two Mobile Services

One for production, one for staging.

#### Set up Git

You don’t want to paste your scripts in the browser. Set up SCM (Git) instead and deploy that way.

(I’ve asked for Mercurial support. I realize that doesn’t matter to most people.)

#### Use Shared Scripts

You can have shared scripts that your API scripts call. When you set up Git, you’ll note that there’s a `shared` folder. Include those (via `require`) from your API files, as in:

<code>var something = require('../shared/something.js');</code>

If you have a function `somefunction` you want made available, in something.js add a line like this:

<code>exports.somefunction = somefunction;</code>

This will make it available from the outside as something.somefunction.

#### Don’t Store Binaries in the SQL Database

[Use blob storage instead](http://inessential.com/2014/04/22/mobile_services_and_blob_storage).

#### Before Deploying

Make sure your files compile. (You should have installed Node.js on your system.) Type <code>node filename</code>. It’ll tell you if there are errors.

#### To Read

Josh Twist has a bunch of blog posts worth reading: [The Twelve Days of Zumo](http://www.thejoyofcode.com/The_twelve_days_of_ZUMO.aspx).

#### If you need an associated website

You can create an Azure Node.js site. You don’t get all the nice parts of Mobile Services, but it’s still Node. That associated website can make API calls to your API server.
