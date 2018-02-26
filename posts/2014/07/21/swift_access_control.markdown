@title Swift Access Control
@pubDate 2014-07-21 11:43:11 -0700
@modDate 2014-07-21 11:43:11 -0700
It’s out, and we have public, internal, and private levels of control.

Public means the world can see it; internal is visible inside a target; private is inside-the-file only. (I think I have this right.)

My first thought: I’m not sure I’ll ever use internal.

My second thought: <em>protected</em> would have been nice. I actually used this in Objective-C, back in the days when we’d declare our instance variables.

My third thought: maybe I don’t really care about protected.

I’ll clarify.

With my Objective-C header files I’m accustomed to thinking about only two levels of access: public and private.

I used to use `@protected` sometimes, back in the days when we declared our instance variables. But I haven’t missed it. And I haven’t even once wished for a target-only access level.

Public-or-private as the only choice imposes a discipline that makes for simpler code. I design for the least-possible surface area, and this makes me think harder about design. If I use internal (or protected) access, then my designs are more complex, and I’m one step away from taking expedient shortcuts at the expense of good design.

So I have classified internal as a code smell and decided not to use it. But this is entirely provisional, because this stuff is all so new, and because I haven’t thought about it as much as the language designers have. I’m a total Swift newbie, like almost everybody else. (I may end up a fan of internal access, in other words, however unlikely that seems right now.)
