---
layout: post
title:  "Why Do We Have Interfaces?"
date:   2022-05-21 17:00:00
categories: [R]
permalink: why-interfaces
description: "Why do we have interfaces?"
---
In most major object-oriented languages like C++, Java, and C#, there are two similar features: interfaces and abstract base classes. In principle, both allow you to specify the API for an object without providing implementations for any (or all) of the methods. Interfaces being basically a "fully" abstract base class, that is, an abstract base class where every method is abstract, not just some. So why would someone use an interface, which offers only a subset of the functionality of an abstract base class?

Abstract base classes are a feature of C++, Java and C#, while interfaces are only available in Java and C#. Java and C# also happen to be the only two of these three languages to only support single, not multiple, inheritance. Interfaces are used in Java and C# to get around the limitations of single inheritance. If you want an object to implement multiple APIs, only one of them can come from a base class, the others must be from interfaces.

In other words, you can make a class that implements as many interfaces as you want in Java and C#, but they can only derive from one base class. Since C++ classes can derive from as many base classes (abstract or not) as they want, interfaces are unnecessary. By limiting classes to single inheritance, Java and C# avoid the issues that can arise from multiple inheritance. When a class inherits from multiple base classes, there's an ambiguity about how you traverse the class inheritance graph. Do you do depth-first search, breadth-first search, or something more complicated? For example, Python uses something called C3 linearization. This problem is sometimes called the "diamond problem" after the diamond-shape class inheritance diagram associated with it. Even when the method resolution order is clear, code can still be difficult to reason about.