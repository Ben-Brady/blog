---
layout: post
title:  "Description of Programming Language Syntax"
date:   2022-12-31 +0000
---

## Significant Whitespace

One of the main downsides of significant whitespace is it's inability to support a usable lambda syntax.

```python
add = lambda a, b: a + b
```

## Function Declaration

There are two primary ways to define a function in a programming language, either they use a keyword such as with python (`def foo()`) or they declare the return type such as with C (`int foo()`).

### Keyword Based

Keyword based function declaration is popular in many modern languages. Additionally, any loosely typed language will often choose this approach.

The keyword for declaring a function can vary greatly depending on the language:

- `fn`: Rust
- `fun`: Kotlin
- `func`: Go
- `function`: Javascript/Lua
- `def`: Python

### Type Based

In languages such as C, C# or java then a function is declared by specifying it's' return type. For this to function it requires that the language be strongly typed. It also forces you to use a simple type as the return type and hinders the usage of generics. The advantage is you can clearly see what type is being returned.

*C*:

```c
void foo() {
    return
}

int bar() {
    return 0
}
```

## Type Hinting

### Declaration Based

*Java*:

```java
float a = 5;
int b = 5;
var c = 5;
```

### Suffix Based

*Rust*:

```rust
let a: u32 = 3
let b: usize = 3
let c = 3
```
