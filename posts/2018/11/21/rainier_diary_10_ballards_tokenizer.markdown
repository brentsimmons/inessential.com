@title Rainier Diary #10: Ballard’s Tokenizer
@pubDate 2018-11-21 13:11:31 -0800
@modDate 2018-11-21 13:11:31 -0800
[Rainier](https://github.com/brentsimmons/Rainier) is the app, and Ballard is the language. It’s named for the neighborhood where I live in Seattle. (Using Pacific Northwest names is what I do now.)

[Ballard](https://github.com/brentsimmons/Ballard) has a fresh GitHub repository. It’s a separate framework, since I want to use it in [NetNewsWire](https://github.com/brentsimmons/NetNewsWire), and because I want to make it so other people can use it in their apps if they want to.

Another goal: the code should be understandable and tinker-able. The idea is to create a language where the implementation is not mysterious, where it’s accessible to even new programmers who are willing to put in some effort.

So I’m writing in Swift, at the highest level I can, and I’m writing blog posts which explain things.

#### Four Pieces

The language implementation will have four main parts:

* **Tokenizer:** takes a string of code and breaks it into _tokens_. A [token](https://github.com/brentsimmons/Ballard/blob/master/Sources/Parser/Token.swift) is a small structure that specifies things like: this is an identifier, and its name is whatever. Or this is an `if` keyword. Or this is a + sign. Etc.
* **Parser:** turns the tokens into a tree of nodes that can be evaluated.
* **Evaluator:** runs the script — that is, it *evaluates* the tree of nodes created by the parser.
* **Standard library:** the set of commands — we call them *verbs* — that are built in to the language. These are for things like operating on strings, files, dates, and so on. This also includes some constants for things like the maximum value of an integer.

Makes sense, no?

#### Where I’m At

On the weekend I got far enough with the [tokenizer](https://github.com/brentsimmons/Ballard/blob/master/Sources/Parser/Tokenizer.swift) — named `Tokenizer` — that I could start writing [tests](https://github.com/brentsimmons/Ballard/tree/master/BallardTests/Tokenizer) for it.

The tokenizer is probably the least interesting part of all of this, and I don’t think I need to write much to explain it.

The gist of it is that it goes through the string by calling `popNextToken()` to create an array of tokens until it reaches the end of the string. It will throw an error if it encounters something it can’t handle.

Which should be super-rare, because the tokenizer does *not* do much in the way of syntax checking. The tokenizer should be able to handle stuff that is entirely incorrect code.

Checking syntax is the job of the parser. The tokenizer just performs that initial pass that gives the parser something besides raw text to work with.

So, next step: write more tests for the tokenizer, fix any bugs, and *then* move on to the parser.

The parser will be more challenging, for sure. The evaluator, too — especially since it needs to be able to handle debugging, which means being able to pause, view the variables in the stack, resume, etc.

But one thing at a time: the tokenizer comes first.
