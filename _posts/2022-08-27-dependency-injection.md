---
layout: post
title:  "Dependency Injection"
date:   2023-08-27 17:00:00
categories: [programming]
permalink: dependency-injection
description: "Dependency Injection"
---

Dependency injection is one of those things I had to look up several times before I was able to internalize the meaning. Which is weird, because it's a programming technique that I've used for longer than I knew there was a word for it. When programming in C, it's common practice---especially when writing libraries---to never allocate memory for data structures within a function.  You let the caller figure out how they're going to allocate memory and have them pass a pointer to that allocated memory to your function. This way, you give the caller flexibility in when and where that memory is allocated.

In high-level languages that manage memory allocation for you, you typically don't need to worry about when and where your memory is allocated. Yet, a similar technique is often used. The allocation and initialization of data structures is often an expensive operation, especially when it involves network communication. So you typically want to avoid doing it more than necessary. If you already have a connection to a database, it's better to reuse it than make another. Therefore, it's often better to pass a function or object the underlying dependencies that it needs rather than having it create those dependencies itself. In addition to being more efficient, dependency injection in high-level languages can give a caller more flexibility around which implementation of a dependency is used for some purpose. If an object depends on another objects that implements some interface, different instances of the first object can use different implementations of that interface.