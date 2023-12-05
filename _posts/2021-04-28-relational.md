---
layout: post
title:  "What's Relational About Relational Databases?"
date:   2021-04-28
categories: [databases]
permalink: relational
description: "What's Relational About Relational Databases?"
---

One things I've noticed about a lot of material on the internet about relational databases is that they very seldom offer a good explanation for what it means for a database to be *relational*. For example, when I Google "what is a relational database", the [first result](https://www.oracle.com/database/what-is-a-relational-database/) (from Oracle no less!) tells us:

> A relational database is a type of database that stores and provides access to data points that are related to one another

To me, this is not a great explanation. Not only is it vague, it's also misleading. The article goes on to clarify this a little, but what it doesn't do is make clear the distinction between two easily confused concepts: the idea of a *relation* in the sense of a relational database, and the idea of a *relationship* between a primary key in one table and a foreign key in another table. It seems to me like there may be some people who use databases every day who are walking around with the mistaken belief that a relational database has something to do with the relationships they allow you to define between primary keys and foreign keys. I should know, because I was once one of those people! But this isn't true: After all, one type of *non-relational* database is a graph database, for which it's ability to define relationships is even *more* central to its data model than relational databases.

So what's a relational database? A database who's data model is centered around relations! What's a relation? Well, it's complicated...

Everyone knows an example of at least one relation: the binary equivalence relation most people refers to as *the equals sign*. The equals sign is a symbol that allows you to write *a = b* and expect that other people know what that means. What does it mean exactly? Well, to a mathematician, it means that the binary tuple *(a, b)* belongs to the subset of R x R that defines the relation. In this case, that subset contains all binary tuples *(a, b)* such that *a = b*. In other words, the infinite set that contains tuple such as *(0, 0)*, *(1, 1)*, *(5.3, 5.3)*, etc.

So how does this relate to databases? Well, relations in the context of database are similar, but different in a few key ways. For one thing, we don't only care about binary tuples but about *n*-ary tuples. For another thing, our relations are finite---not infinite---sets, these are called *finitary* relations. You can imagine if you wanted to write out the definition of an *n*-ary, finitary relation, you could just list the elements in the set, after all there's only so many of them. So let's say you had a relation that is defined by all integer solutions to the equation *a + b + c = 2* for non-zero *a, b, c*. You could write out the set as:
```
{
    (0, 0, 2),
    (0, 1, 1),
    (0, 2, 0),
    (1, 1, 0),
    (1, 0, 1),
    (2, 0, 0)
}
```

What is this starting to look like? A table! What do relational databases store? Tables! The reason that relational databases are relational is because their data model is based around tables. In other words, the simplest definition of a relation in the context of databases is *a table*. It just so happens that relations can have relationships with other relations in a relational database, but this isn't why it's relational.

So a better first sentence in Oracle's documentation would be:

> A relational database is a type of database that stores and provides access to data represented as tables