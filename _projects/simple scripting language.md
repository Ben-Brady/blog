---
title: "Simple Scripting Language"
date: 2023-02-10 +0000
image: 
  path: /images/ssl.png
  thumbnail: /images/ssl.png
  caption: "Simple Scripting Language"
---

A scripting language I wrote i made to learn more about interpreters and parsers. [Repository](https://github.com/Ben-Brady/simple-scripting-language)

## Language

I based the language of Rust's snytax however, I designed it have very few fundemental concepts, but derive complexity from that. For instance, everything yields a value. Every single statement is also an expression. This allowed you do this such as assign variable based on the result value of an if statement.

A lot of things are missing from the language to make it of any use, such as control flow, functions, or anything complex. I'm planning on expanding on this in future with another language.

## Design

The interpeter works in 3 parts: the lexer, the parser, and the interpreter.

The lexer takes the incoming file or text and tranforms it into a series of tokens. This makes it easier to work with not having to worry about formatting or whitespace in the parser. One of the issues I ran into was that if something became with the same text as a statement such as `letter` it would be interpreted. This was caused by me not requireing whitespace.

The parser takes a stream of tokensant turns them into a simplistic tree. This does most of the heavy lifting as forms the actual layout of the program. This was the hardest part to write as I struggled a lot with the complexity of the rules. For instance, blocks were quite hard to implement as it was hard to seperate blocks and statements apart.

The final part is the intepreter, which simplys runs the abtract tree as code. This was actually the easiest part of the program as the AST does most of the heavy lifting. It simply follows through with each expression and checks to see if it should run it.
