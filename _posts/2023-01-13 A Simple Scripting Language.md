---
layout: post
title:  "A Simple Scripting Language"
date:   2023-01-13 +0000
---

One of the project that I hope to undertake soon is writing a simple programing language.

## Scope
- Variables/Literals `let a = 1`
- Integers, Boolean
- if/else
- comparison operators: `== != > >= < <=`
- boolean operators: `|| && !`
- mathematical operators: `+ - / * ** %`
- print: `print`

## Example

```
let a = 1;
if a ** 2 == 4 {
  print a;
} else {
  print false;
}
```

## Syntax Tree
- statement
	- Assignment
		- variable: `num`
		- value: `1`
- if statement
	- condition
		- binary operator
			- op: `comparison`
			- a
				- binary operator
					- a
						- Variable: `num`
					- b
						- Literal: `2`
			- b
				- Literal: `4`
	- branch
		- statement
			- print
				- variable: `num`
	 - else 
		 - statement
			 - print
				 - Literal: `false`
