---
layout: post
title:  "The Boyer–Moore majority vote algorithm"
date:   2023-12-05
categories: [algorithms]
permalink: majority-vote
description: "The Boyer–Moore majority vote algorithm"
---

Let's say you have a stream of elements of unbounded size. You know that one element appears a majority of times. Can you find that majority element in a single scan using constant memory? There's an interesting algorithm to do this called the [Boyer–Moore majority vote algorithm](https://doi.org/10.1007/978-94-011-3488-0_5). 