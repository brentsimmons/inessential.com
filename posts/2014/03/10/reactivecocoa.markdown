@title ReactiveCocoa
@pubDate 2014-03-10 10:35:18 -0700
@modDate 2014-03-10 10:45:25 -0700
Me on Twitter [last Saturday](https://twitter.com/brentsimmons/status/442451689946095616), when asked about [ReactiveCocoa](https://github.com/ReactiveCocoa/ReactiveCocoa):

>It’s a research experiment, and I’m glad it’s happening, but I myself wouldn’t use it in production code at this point.

This may sound dismissive, though that wasn’t my intention. ReactiveCocoa is important, and I’m glad it’s happening for two reasons:

1. Functional reactive programming looks more and more like an important part of the future of programming.

2. Research that can change how we build apps should happen not just inside Apple but outside too.

Some extremely intelligent people are working on this. I applaud and encourage them to find better ways to do what we do.

Because ReactiveCocoa is more ambitious than the average open source project, because it seeks to change at a fundamental level how we write Cocoa apps, because it’s applying the principles of functional reactive programming to a language and framework that’s only somewhat cooperative, I consider it a research project.

And I won’t use it in my production code. Not yet. (I’m the weirdo who can’t even quite bring himself to use Core Data.)

Here’s why. It has nothing to do with code quality. Rather, there’s a trade-off involved in using ReactiveCocoa that I’m not ready to make.

Remember that there are two ways to write bug-free code: 1) use techniques that make bugs less likely, and 2) write code that you can read and verify for yourself is bug-free.

(Obviously you should use both.)

I’ll borrow an example from NSHipter’s [article on ReactiveCocoa](http://nshipster.com/reactivecocoa/) (which you should read if you haven’t already).

Here’s some conventional code:

<code>- (BOOL)isFormValid {</code><br />
<code>&nbsp;&nbsp;return [self.usernameField.text length] > 0 &&</code><br />
<code>&nbsp;&nbsp;&nbsp;&nbsp;[self.emailField.text length] > 0 &&</code><br />
<code>&nbsp;&nbsp;&nbsp;&nbsp;[self.passwordField.text length] > 0 &&</code><br />
<code>&nbsp;&nbsp;&nbsp;&nbsp;[self.passwordField.text isEqual:self.&#8203;passwordVerificationField.text];</code><br />
<code>}</code><br />
<code></code><br />
<code>#pragma mark - UITextFieldDelegate</code><br />
<code></code><br />
<code>- (BOOL)textField:(UITextField \*)textField</code><br />
<code>&nbsp;&nbsp;shouldChangeCharactersInRange:(NSRange)range</code><br />
<code>&nbsp;&nbsp;replacementString:(NSString *)string</code><br />
<code>{</code><br />
<code>&nbsp;&nbsp;self.createButton.enabled = [self isFormValid];</code><br />
<code></code><br />
<code>&nbsp;&nbsp;return YES;</code><br />
<code>}</code>

Here’s the same thing using ReactiveCocoa:

<code>RACSignal \*formValid = [RACSignal</code><br />
<code>&nbsp;&nbsp;combineLatest:@[</code><br />
<code>&nbsp;&nbsp;&nbsp;&nbsp;self.username.rac\_textSignal,</code><br />
<code>&nbsp;&nbsp;&nbsp;&nbsp;self.emailField.rac\_textSignal,</code><br />
<code>&nbsp;&nbsp;&nbsp;&nbsp;self.passwordField.&#8203;rac\_textSignal,</code><br />
<code>&nbsp;&nbsp;&nbsp;&nbsp;self.passwordVerificationField.&#8203;rac\_textSignal</code><br />
<code>&nbsp;&nbsp;]</code><br />
<code>&nbsp;&nbsp;reduce:^(NSString \*username, NSString \*email, NSString \*password, NSString \*passwordVerification) {</code><br />
<code>&nbsp;&nbsp;&nbsp;&nbsp;return @([username length] > 0 && [email length] > 0 && [password length] > 8 && [password isEqual:passwordVerification]);</code><br />
<code>&nbsp;&nbsp;}];</code><br />
<code></code><br />
<code>RAC(self.createButton.enabled) = formValid;</code>

After so many years of writing Cocoa code, I can read and understand the conventional version easily. The ReactiveCocoa version is very different from the code I’ve been writing all along, which makes it much harder for me to verify <em>by reading</em> that it’s correct.

That’s a choice every developer has to make. You may be willing to take the time to learn this so well that the ReactiveCocoa version reads naturally and easily. Me, I’m not willing, at least not yet.

(This assumes I’ve taken step one, which is to research functional reactive programming well enough so that I’m convinced of its benefits. I haven’t done so, though I’ve done enough reading to lean toward thinking it does have benefits.)

Here’s what may happen: ReactiveCocoa gains popularity, and it demonstrates that functional reactive programming is, in important respects, a better way to write apps. And then Apple — because only Apple can do this part — adds framework and language support, and does so in a way that makes for easily-readable code.

That’s my hope.

I most emphatically do *not* believe progress has stopped. There *are* better ways to do what we do, and everybody who’s trying to find these better ways has my thanks.

PS *Highly* recommended: Rob Rix on [Postmodern Programming](https://github.com/robrix/Postmodern-Programming/blob/master/Postmodern%20Programming.md). I’ve read it twice already.
