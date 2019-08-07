@title Implementing Single-Key Shortcuts in NetNewsWire
@pubDate 2019-03-05 21:09:22 -0800
@modDate 2019-03-05 21:13:32 -0800
NetNewsWire supports using single-key shortcuts for some commands: the `k` key marks all as read, for instance. The space bar scrolls the current article, or goes to the next unread if there’s nothing more to scroll.

There are a bunch of these, and they’re documented: see NetNewsWire Help menu > Keyboard Shortcuts.

These kinds of shortcuts are fairly rare in Mac apps, and rightly so — they’re best for apps where power users might need to process a bunch of stuff and move around quickly. That doesn’t describe every app (thank goodness!).

Since this isn’t really a standard AppKit thing, you might wonder how I implemented this in NetNewsWire.

#### Getting keyboard events

You have to override `keyDown(with event: NSEvent)` — so NetNewsWire has subclasses such as [SidebarOutlineView](https://github.com/brentsimmons/NetNewsWire/blob/master/NetNewsWire/MainWindow/Sidebar/SidebarOutlineView.swift) in order to get keyboard events.

I *could*, if I wanted, just get the character from the event and do a `switch` statement with code like this:

	case 'k':
		markAllAsRead()

This gets ugly pretty quickly, and, importantly, I plan to make keyboard shortcuts customizable (at some point), so I chose a different path.
 
#### Property List Files

If they’re customizable, then the specifiers need to be stored in some data format. Property lists (plists) are a good choice, since they’re easy to read and edit in Xcode.

Now, I’m not making them customizable yet, but I figured it would be smart to use the same format and implementation for the default sets of shortcuts.

#### Inside the plists

There are a few plist files: one for global shortcuts, one for the sidebar, one for the timeline, etc. (I could have made just one file, but I didn’t. Doesn’t matter.)

Each file contains an array of shortcuts; each shortcut has a `key` and an `action`. The key is the actual key, such as `k` or `'` — or a placeholder such as `[rightarrow]` where the actual key couldn’t be listed in the plist. (The app translates placeholders into their actual values.)

A shortcut may also have one or more modifiers, and those are represented as booleans: `shiftModifier`, for instance. This way we can differentiate between the space key and shift-space.

The `action` part is a string specifying which method to call for the given shortcut.

Here’s an [example of one of those files](https://github.com/brentsimmons/NetNewsWire/blob/master/NetNewsWire/MainWindow/Keyboard/GlobalKeyboardShortcuts.plist).

#### The keyDown implementation

`SidebarOutlineView ` overrides `keydown`:

	override func keyDown(with event: NSEvent) {
		if keyboardDelegate.keydown(event, in: self) {
			return
		}
		super.keyDown(with: event)
	}

The `keyboardDelegate` gets the first shot at handling the key. If it doesn’t handle it, then normal processing continues.

#### SidebarKeyboardDelegate

There are several keyboard delegates, but let’s look at [SidebarKeyboardDelegate](https://github.com/brentsimmons/NetNewsWire/blob/master/NetNewsWire/MainWindow/Sidebar/Keyboard/SidebarKeyboardDelegate.swift), since these all work about the same.

In `init` it reads its keyboard shortcut definitions from a plist in the app bundle and creates a `Set<KeyboardShortcut>`. A [KeyboardShortcut](https://github.com/brentsimmons/RSCore/blob/master/RSCore/Keyboard.swift) is a `KeyboardKey` (defined in same file) plus an action string.

A `KeyboardKey` describes the key, including its integer value and any combination of modifiers (shift, option, command, control).

In keyDown, `SidebarKeyboardDelegate` first gives [MainWindowKeyboardHandler](https://github.com/brentsimmons/NetNewsWire/blob/master/NetNewsWire/MainWindow/Keyboard/MainWIndowKeyboardHandler.swift) a chance to handle the key. `MainWindowKeyboardHandler` handles keys that are global across views.

If `MainWindowKeyboardHandler` doesn’t handle it, then it looks for a `KeyboardShortcut` that matches the pressed key.

	let key = KeyboardKey(with: event)
	guard let matchingShortcut = KeyboardShortcut.findMatchingShortcut(in: shortcuts, key: key) else {
		return false
	}

If it finds a matching shortcut, then it makes the shortcut do the thing it’s supposed to do:

	matchingShortcut.perform(with: view)

#### Performing the shortcut

Remember that a `KeyboardShortcut` has a `KeyboardKey` and an `actionString`. That string is pulled from the plist: it’s something like `nextUnread:` or `openInBrowser:`.

We turn this into a selector using `NSSelectorFromString` and store it in a local variable `action`.

(The Objective-C runtime has a particularly beautiful thing: messages are real things, and they exist separately from objects.)

The `perform(with:)` method looks like this:

	public func perform(with view: NSView) {
		let action = NSSelectorFromString(actionString)
		NSApplication.shared.sendAction(action, to: nil, from: view)
	}

Here’s Apple’s documentation on [NSApplication.shared.sendAction](https://developer.apple.com/documentation/appkit/nsapplication/1428509-sendaction).

The short version of what it does: if `to` (the target) is nil, it starts with the first responder, then checks its nextResponder, then its nextResponder, and so on until it finds an object that *responds* to the specified selector (the action) — and then it asks that object to perform that method (or: it sends that message to the receiver). (It also checks the window’s delegate and some other things before giving up, when it gets that far.)

This means, for instance, that I don’t have to implement `openInBrowser:` in `SidebarOutlineView`. It could be implemented in its view controller, in `MainWindowController`, etc., as long as there is an implementation in the responder chain.

This way the implementation can be placed where it makes sense. I can even move `openInBrowser:` without needing to change the plist configuration.

And — this is important — it means that there might be (and there are, in NetNewsWire) *multiple* implementations of `openInBrowser:`. The sidebar has one which opens the home page of the selected feed. The timeline has a different one which opens the URL for the selected article.

The one that gets called is based on which one of these is the first responder, because that’s where the responder chain starts. (Which is another way of saying: the implementation that gets called is based on what thing has user focus.)

Both of these `openInBrowser:` commands are represented by the same `KeyboardShortcut` from the global keyboard shortcuts plist.

#### Not Magic

It may seem like `NSApplication.shared.sendAction` is doing something reserved for Apple that you couldn’t do, or couldn’t do easily.

But you could actually write this yourself. This simple version (which just checks `nextResponder`) has all the critical bits.

	func sendAction(_ action: Selector, to target: Any?, from sender: Any?) -> Bool {
		var responder = NSApplication.shared.keyWindow?.firstResponder
		while responder != nil {
			if responder?.responds(to: action) ?? false {
				responder?.perform(action, with: sender)
				return true
			}
			responder = responder?.nextResponder
		}
		return false
	}

Obviously we don’t have the source to `NSApplication.shared.sendAction` — but, at least in concept, that’s all it’s doing. (Minus the part where it checks some things after exhausting `nextResponder`.)

#### Summary

In a Mac app, how does the Edit menu‘s Copy command know what to do? It walks the responder chain: the first to claim that it responds to the `copy:` message then performs the `copy:` method.

You don’t have just one `copy:` method somewhere that has to figure out the context (figure out what has focus) and then do the right thing. Instead, you may have multiple `copy:` methods.

(This is much less of a thing on iOS. But when you go to use Marzipan with your iOS apps, there’s a good chance you’re going to need to know about this.)

The Copy command (and others) use the same pattern I’m using here, in other words.

It’s also worth thinking about how nibs and storyboards actually get loaded by your app. All the wired-up actions are, at some level, just strings — so the frameworks (UIKit and AppKit) use `NSSelectorFromString` to turn these strings into real messages.

Having an idea of how all this works under-the-hood is useful knowledge: it means you understand your app better. It also means that when you’re faced with something like implementing a keyboard shortcuts system, you’ll have the right tools for the job.

(Of course this isn’t the right tool for every job.)

#### PS Try this!

In Xcode, set a symbolic breakpoint for `NSSelectorFromString`. Make the Action a sound. Check the box next to “Automatically continue after evaluating actions” — this way it won’t actually stop.

Now launch your app. Even if *you* don’t ever use this, your app sure does!

And, for bonus points, also set a similar breakpoint for `NSClassFromString`. Give it a different sound.
