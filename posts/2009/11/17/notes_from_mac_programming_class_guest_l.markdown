@title Notes from Mac programming class guest lecture
@pubDate Tue Nov 17 09:44:33 -0800 2009
@modDate Tue Nov 17 09:48:37 -0800 2009
Last night I gave a guest lecture at Hal Mueller’s <a href="http://www.extension.washington.edu/ext/certificates/iph/iph_gen.asp">Mac programming class</a> at the UW Extension.

The idea behind the lecture was to talk about what makes a great Mac app. I took that as an excuse to talk about everything from work habits to UI to marketing. In other words, I threw in just about everything I know — which, it turns out, only takes about an hour to deliver. :)

It goes chronologically — getting to 1.0, releasing 1.0 and the follow-through, on to working on 2.0.

I don’t actually have time right now to write it up properly. But, at least, here are my notes:

### Road to 1.0

More money to make in Mac software than in iPhone software

Mission statement<br />
Photoshop example

#### Work habits
stay in the chair<br />
will have to give up things - games<br />
exercise is very good for brain and morale

motivation - gumption<br />
think of thing you want, rationalize that this is how you get it<br />
fear is good too

nearby small notebook works as short-term memory and to-do lists<br />
break tasks down real small

#### Design

keep 1.0 feature list very, very small<br />
polish the hell out of those features<br />
you don't really know what users will ask for

Pretend you're a toy-maker - Kris Kringle<br />
Delight your users<br />
Peacock feathers<br />
Do lots with one click<br />
The extra step to make things easy<br />
Feedback - animations - never "what just happened?"<br />
Performance is UI<br />
Stability is job #1<br />
Look at lots of other apps, esp. by those you admire, but also look at apps that don't work as well<br />
Coherency of UI<br />
Going beyond the merely utilitarian means you understand the human spirit - and your app is more usable and thus more useful

Sketch out UI<br />
Use Acorn or whatever to do actual mockups<br />
Cabel Sasser working on Coda

Shoot for ADAs and Eddys - by that I mean: don't pander, just aim high<br />
wwad<br />
wwpd

#### Code

unit tests<br />
version control<br />
bug tracker

Support latest OS, not OS minus one, on major releases<br />
use latest technologies<br />
Multi-threading only if you have to<br />
AppleScript support might make sense

Automate builds, etc.<br />
Pay attention to repeated stuff - maximize productivity, minimize errors

don't fight frameworks<br />
learn the Cocoa way<br />
Don't subclass very much, at least not beyond one level<br />
Don't waste time on wrappers<br />
Don't over-use categories<br />
Pretend someone else who knows Cocoa will use your code

architecture is important<br />
write it down

Error checking -- with recovery when possible<br />
Especially important if works with cloud

Use Sparkle<br />
Use Growl

#### Beta testing

Hallway UI testing -- wife, husband, kid, cat

don't do public betas<br />
get beta testers<br />
remember they're geeky

Have crash logs sent back to you

Use Shark and Instruments

Random testing

Charge enough money for your app: $19.95 usually a minimum

File bugs with Apple


### 1.0 Release and marketing

listening to users<br />
remember that people who actually submit request may, on average, be slightly geekier than the entire population<br />
Good stories are important<br />
never panic and add a feature<br />
Use Twitter - for you *and* for product<br />
Have forums or mailing list or something<br />
Have weblog - point to other cool stuff, not just yours<br />
Be human<br />
There will always be complaints. Pretend to yourself that you have a thick skin.<br />
Don't make promises before shipping<br />
Keyword searches for your app

Give back to dev community if possible<br />
Other developers also have influence<br />
Go to WWDC etc.<br />
Read developers weblogs

Let world know what you're working on in general - don't need details

Take the long view


### 2.0 and up

it's okay to have users wanting more<br />
it's okay to bring your users along - make simple things a little more complex later on

Some great-seeming architectures are hard to remember and understand<br />
Don't be afraid to re-architect

remove features

Keep learning

I will make mistakes, sometimes a series of them. You will make mistakes. And some of what I've said is wrong, or wrong for you or your app.
