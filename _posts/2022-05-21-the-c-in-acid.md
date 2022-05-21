---
layout: post
title:  "The C in ACID"
date:   2022-05-21 10:30:00
categories: [databases]
permalink: the-c-in-acid
description: "What does the C in ACID mean?"
---

If you're anything like me, at some point you've had the following thought:

> According to the CAP theorem, some databases are consistent (CP) and some are highly available (AP). How do I know which are which? Well, a database that supports ACID transactions must be consistent. After all, it's right there in the C of ACID!

But, like me, you would be wrong. 

The C in CAP refers to consistency between nodes in a multi-node system. However, the C in ACID can apply to single-node relational databases. 

In chapter 7 of *Designing Data-Intensive Systems*, Martin Kleppmann distinguishes between the C in CAP, which is sometimes referred to as *linearizability*, and the C in ACID, which is about *maintaining invariants* in your data, such as the balancing of credits and debits in an accounting system. Check out [this](http://jepsen.io/consistency) diagram if you want to understand how complicated things can really get. The two most important terms are linearizability (CAP consistency) and serializability, which I believe is equivalency to the strongest version of ACID isolation.

In contrast to linearizability, invariant maintenance isn't actually something that databases can enforce most of the time. While it's an important property of many data systems, it's often something that has to be enforced at the application level rather than the database level. The exceptions referential integrity constraints and unique constraints, which databases can enforce. Ultimately, Kleppmann concludes that

> Atomicity, isolation, and durability are properties of the database, whereas consistency (in the ACID sense) is a property of the application. The application may rely on the database’s atomicity and isolation properties in order to achieve consistency, but it’s not up to the database alone. Thus, the letter C doesn’t really belong in ACID.

In other words, the C in ACID is basically a misnomer. Maybe AID didn't sound as cool as ACID. Either way, it's really only a concept that makes sense when you're thinking about your system as a whole, not your database in particular.