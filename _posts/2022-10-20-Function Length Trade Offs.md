---
layout: post
title:  "Abstraction Trade-Offs"
date:   2022-10-20 +0000
---

My stance on code splitting has changed over the years. I orinally wrote long unreadable functions like most devs, however after getting and reading Uncle Bob's book I started to write very short functions. Once again I'm starting to re-evaluate this system.

Say you have a long function, common practice dictates that you should split it up into several smaller functions. However, it cuts both ways. The advantage of abstraction is also it's downside, it hides the implemntation. The problem is that it makes it hard to identify what your code is actually doing if it's abstracted away from you. This can mean it's hard to visualise the side effects of a block of code or how performance intensive it actual is. In some cases where your only doing something once, a long function can actually be quite useful for giving you an overview of execution.

Although on the other hand, writing many big blocks of code can easily become unreadable as your skim past it. It's all about striking a balance, abstracting out tasks into functions and reserving long big blocks of code for special cases.

### Advantages

- Reduced indentation
- Shows clear dependencies
- Abstracts a task
- Increased Testability

### Disadvantages

- Muddies the logic
- Reliquishes Control
