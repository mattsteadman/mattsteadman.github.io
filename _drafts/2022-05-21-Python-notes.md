---
layout: post
title:  "Python Notes"
date:   2022-05-21 10:30:00
categories: [programming, notes]
permalink: Python-notes
description: "Some interesting things I've learned about Python recently"
---


I've recently been learning a lot about Python. Here are some interesting things I've learned recently.

- What's the difference between `@classmethod` and `@staticmethod`? `@classmethod` gets the it's class (`cls`) as implicit first argument. This means that it can modify class state if it wants. Static methods doesn't get it's class as an argument.

- Python supports generic function in the style of R S3 methods through the `@singledispatch` decorator.

- If you need to iterate through something in reverse, use `reversed()`.

- If you need to iterate through two things at once, use `zip()`. It will stop iterator when the smaller of the two iterators stops.

- The general term for a piece of data that singles end of data, like a `\0` terminator in C, is a sentinel value. Notice that this is an example of old-style in-band signalling, rather than new-style out-of-band signalling, like an extra attribute (size) or exception (`StopIteraton`).
	- In python, you can automatically convert an sentinel value to a `StopIteration` by passing it as the second argument to `iter()`.

- Partial function application is easy in Python. Just use `functools.partial()`.

- Every argument in a Python function can be either positional or keyword unless you explicitly indicate otherwise. To indicate the *end* of positional-only arguments, use the `/` argument. To indicate the *beginning* of keyword-only arguments, use the `*` argument.


- Use `namedtuple`s to improve readibility as an alternative to `enum.Enum`.

- If you find yourself adding/removing items from the beginning of a list with `del`, `.pop(0)` or `.insert(0, item)`, then you should be using a `deque`.

- Use `contextlib.suppress(e)` to temporarily suppress an exception.

- To terminate a generator, never do `raise StopIteration`. This won't work anymore. Instead, simply use `return`.

- "Frozen" doesn't really have a special meaning in Python aside from immutable.

- Heaps offer a similar kind of partial ordering that you get in a tournament bracket.