@title Post-WWDC Thoughts on Rebooting Frontier
@pubDate 2014-06-16 10:42:47 -0700
@modDate 2014-06-16 10:46:40 -0700
(Note: this is all thought experiment. I have no idea if anything will ever get done.)

I’ve got Sal’s presentation on JavaScript for Automation playing right now. It seems obvious to me that that’s the language. 

But I’m mainly thinking about the highest level. What are Frontier’s core virtues?

* Easy persistence in a hierarchical database with a GUI browser that has great navigation.

* One central location (an app) with quick access to your database, scripts, scheduled scripts, suites of scripts, static websites, and dynamic websites and web services.

* Extendable and scriptable UI. A suite can add a menu, for instance.

* Development and runtime environments are the same thing.

There are plenty of cool things about Frontier that aren’t strictly required. Do scripts *have* to be written in an outliner? No. It’s a cool thing, but it’s not critical. Scripts don’t even have to live in the database — in fact, it might be better if they didn’t. Keep the database to data only. What *is* critical is that the app makes viewing and editing scripts convenient and easy, and it’s just as easy to see the data that scripts work with, side-by-side with the scripts themselves.

Back to high-level thinking. I’m thinking about File > New. What might a scriptor need to create?

* Quick script: a disposable one-line (or few-line) script.

* Simple script: a one-file script that does a thing. You’d want to get back to it and run it any time.

* Suite: a set of related scripts. A mini-app.

* Library: a set of related scripts that other scripts can call. Might be a scripting interface to another app, might be commands that drive a server, might be wrappers for some Cocoa APIs, etc.

* Scheduled script: runs periodically. Probably calls into a suite or a library.

* Static website: a set of data and scripts that is turned into a website by a static website rendering suite.

* Dynamic website/web-services: a set of data and scripts that is turned into a website (and/or API endpoints) by a dynamic website rendering suite.

The thing is, these aren’t necessarily discrete things. You might want to build a system with a library, a scheduled script, and a dynamic website (for instance). Imagine a local RSS reader: it has an RSS parsing library, an RSS storage library, a scheduled script that downloads a bunch of feeds, and a dynamic website that provides the feed-reading UI.

The app should encourage developing in layers, but it should also make it easy to associate these layers, so you can work on that RSS reader (for instance) as a whole.

The other thing is, sometimes you really do just want to create a library or static website or whatever. But then later you might want to add a scheduled script to your website (for instance), and you’ll want those things to be associated.

In later years Frontier developed a higher-level system of Tools. Tools could contain all of these things.

The name “Tools” is Windows-y and isn’t great for a Mac app. (Which is, no question, what I’m thinking about. I have zero interest in writing for Windows or Linux.) In the year 2014 I think we just use the name “App” for something like this, even though it’s a bit of overloading. I’d argue that it’s the approachable and understandable name.

So your choices would be:

File > New > App<br />
File > New > Script<br />
File > New > Scheduled Script

The UI for your app would allow you to add and edit a library of scripts, scheduled scripts, menu, static website, and dynamic website. Each part would be optional.

But there’s a different approach I could take instead, a project-based approach. In this case an app is more like an IDE project, and you can add things — new things and existing things — to the project.

Consider the scenario where you have multiple apps that use the same RSS parser library. You’d want that library associated with each app, rather than just owned by a single app.

So maybe it would be:

File > New > Project<br />
File > New > Library<br />
File > New > Script<br />
File > New > Scheduled Script<br />
File > New > Static Website<br />
File > New > Dynamic Website

After creating a thing, you can add it to one or more projects.

This makes a project much looser than an app: it’s really just a UI thing, a visible, clickable, navigable organization of separate things. And that makes packaging and distribution more difficult, where an app would be a contained thing and easier to distribute.

I don’t know. Still thinking.

But I’m convinced — in part because people keep coming up to me and telling me so — that there’s a value in File > New > Thing That I Want to Make.
