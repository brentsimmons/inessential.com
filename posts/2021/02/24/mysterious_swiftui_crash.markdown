@title Mysterious SwiftUI Crash
@pubDate 2021-02-24 11:21:39 -0800
@modDate 2021-02-24 11:32:37 -0800
A friend just released a new version of their app — and it has a new crash not seen during development.

This new version of the app has a bunch of new SwiftUI code, and this crash is definitely in SwiftUI — but it’s apparently in SwiftUI itself.

Anyone else seen this? Is there something my friend can do to work around this?

	Hardware Model: iPhone13,4
	Code Type: ARM-64
	OS Version: iPhone OS 14.4 (18D52)
	
	Exception Type: SIGTRAP
	Exception Codes: TRAP_BRKPT at 0x19d447a18

	Crashed Thread: 0

	Thread 0 Crashed:
	0 libswiftCore.dylib 0x000000019d447a18 _assertionFailure(_:_:file:line:flags:) + 492
	1 SwiftUI 0x00000001a011c52c ViewCache.commitPlacedChildren(from:to:) + 3032
	2 SwiftUI 0x000000019ffc8eb4 specialized IncrementalChildPlacements.updateValue() + 1384
	3 SwiftUI 0x00000001a00e6fbc partial apply for specialized + 24
	4 AttributeGraph 0x00000001c2cbba50 AG::Graph::UpdateStack::update() + 492
	5 AttributeGraph 0x00000001c2cbbe84 AG::Graph::update_attribute(AG::data::ptr<AG::Node>, bool) + 332
	6   AttributeGraph 0x00000001c2cc5088 AG::Subgraph::update(unsigned int) + 884
	7 SwiftUI 0x00000001a07d1cdc GraphHost.runTransaction() + 172
	8 SwiftUI 0x00000001a07d4e1c GraphHost.runTransaction(_:) + 92
	9 SwiftUI 0x00000001a07d37a8 GraphHost.flushTransactions() + 176
	10 SwiftUI 0x00000001a07d4db4 closure #1 in closure #1 in GraphHost.asyncTransaction<A>(_:mutation:style:) + 24
	11 SwiftUI 0x00000001a02a3168 partial apply for closure #1 in ViewGraphDelegate.updateGraph<A>(body:) + 28
	12 SwiftUI 0x00000001a0726e9c closure #1 in ViewRendererHost.updateViewGraph<A>(body:) + 108
	13 SwiftUI 0x00000001a071de7c ViewRendererHost.updateViewGraph<A>(body:) + 92
	14 SwiftUI 0x00000001a029f6d0 ViewGraphDelegate.updateGraph<A>(body:) + 80 
	15 SwiftUI 0x00000001a07d4d84 closure #1 in GraphHost.init(data:) + 124 
	16 SwiftUI 0x00000001a07d66f0 closure #1 in GraphHost.asyncTransaction<A>(_:mutation:style:)partial apply + 40
	17 SwiftUI 0x00000001a02c2b98 thunk for @escaping @callee_guaranteed () -> () + 28
	18 SwiftUI 0x000000019ff91a10 static NSRunLoop.flushObservers() + 148
	19 SwiftUI 0x000000019ff91974 closure #1 in closure #1 in static NSRunLoop.addObserver(_:) + 16
	20 SwiftUI 0x000000019ff8c4b4 specialized thunk for @callee_guaranteed () -> (@error @owned Error) + 24
	21 libswiftObjectiveC.dylib 0x00000001bfcc3f30 autoreleasepool<A>(invoking:) + 64
	22 SwiftUI 0x000000019ff91954 closure #1 in static NSRunLoop.addObserver(_:) + 64
	23 SwiftUI 0x000000019ff91aac @objc closure #1 in static NSRunLoop.addObserver(_:) + 56
	24 CoreFoundation 0x0000000199798358 __CFRUNLOOP_IS_CALLING_OUT_TO_AN_OBSERVER_CALLBACK_FUNCTION__ + 36
	25 CoreFoundation 0x00000001997925c4 __CFRunLoopDoObservers + 576
	26 CoreFoundation 0x0000000199792b74 __CFRunLoopRun + 1056
	27 CoreFoundation 0x000000019979221c CFRunLoopRunSpecific + 600
	28 GraphicsServices 0x00000001b135e784 GSEventRunModal + 164
	29 UIKitCore 0x000000019c1d2ee8 -[UIApplication _run] + 1072
	30 UIKitCore 0x000000019c1d875c UIApplicationMain + 168
	31 AppName 0x0000000100ed8444 main (main.m:19)
	32 libdyld.dylib 0x00000001994526b0 start + 4
