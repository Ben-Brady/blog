---
layout: post
title:  "Function Length Trade-Offs"
date:   2022-10-20 +0000
---

My stance on code splitting has changed over the years. I orinally wrote long unreadable functions like most devs, however after getting and reading Uncle Bob's book

Whether or not it's important to see the logic or implementation

Say you have a long function, common practice dictates that you should split it up into several smaller functions. However, it cuts both ways. The advantage of *code splitting* is also it's downside, it hides the implemntation. In most cases this is useful, hhowever as you get to a low point in your code where it's all about implementation, *code splitting* can seriously hinder you ability to se

## Code Splitting

### Advantages

- Reduced indentation
- Shows clear dependencies
- Abstracts a task
- Increased Testability

### Disadvantages

- Muddies the logic
- Reliquishes Control
