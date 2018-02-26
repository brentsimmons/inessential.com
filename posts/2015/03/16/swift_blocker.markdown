@title Swift Blocker
@pubDate 2015-03-16 21:23:15 -0700
@modDate 2015-03-16 21:27:54 -0700
I did some work to switch Vesper over to frameworks. In a framework I built for FMDB, a public header file has the following line:

<code>#import "sqlite3.h"</code>

That’s not allowed by default. But there’s an Xcode setting for it: “Allow Non-modular Includes in Framework Modules.”

This setting is the user-friendly version of CLANG&#8203;\_ALLOW&#8203;\_NON&#8203;\_MODULAR&#8203;\_INCLUDES&#8203;\_IN&#8203;\_FRAMEWORK&#8203;\_MODULES. Here’s what Xcode’s Quick Help has to say:

>Enabling this setting allows non-modular includes to be used from within framework modules. This is inherently unsafe, as such headers might cause duplicate definitions when used by any client that imports both the framework and the non-modular includes themselves.

Okay. I understand the issue and I’m willing to press the button — and I did, and everything works. Great.

Well, until I added some Swift code that imports that framework. Then I get the error:

>Include of non-modular header inside framework module 'FMDB.FMDatabase'

Swift apparently doesn’t respect the CLANG&#8203;\_ALLOW&#8203;\_NON&#8203;\_MODULAR&#8203;\_INCLUDES&#8203;\_IN&#8203;\_FRAMEWORK&#8203;\_MODULES setting, while Objective-C does.

Filed as <a href="rdar://20184784">rdar://20184784</a>.

The bug report includes a small sample project that you can download: <a href="http://ranchero.com/downloads/NonModularBug.zip">NonModularBug.zip</a>.

#### Why I’m blocked

The VesperData framework — where VSNote, VSTag, and VSAttachment live — depends on QSDB (similar in purpose to <a href="https://github.com/marcoarment/FCModel">FCModel</a>) which depends on <a href="https://github.com/ccgus/fmdb">FMDB</a>.

The upshot is that I can’t write any Swift code that references the data model. Which doesn’t leave me a whole lot else. (Given what’s already completed or at least started as Objective-C files.)

(Half of my friends — Gus included — are shouting at the monitor that this is a *feature* of FMDB and I should take it as a sign.)
