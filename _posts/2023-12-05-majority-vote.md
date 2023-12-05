---
layout: post
title:  "The Boyer–Moore Majority Vote Algorithm"
date:   2023-12-05
categories: [algorithms]
permalink: majority-vote
description: "The Boyer–Moore majority vote algorithm"
---

Let's say you have a stream of elements of unbounded size. You know that one element appears a majority of times. Can you find that majority element in a single scan using constant memory? There's an interesting algorithm to do this called the [Boyer–Moore majority vote algorithm](https://doi.org/10.1007/978-94-011-3488-0_5).

The paper on this algorithm explains the idea behind it using a convention center filled with delegates for some political candidate. We imagine that the "voting" happens like this: delegates can knock each other down to cancel out the vote of an opponent, however the knocker also gets knocked down too. The candidate with the last delegate(s) standing wins. Assuming there is some candidate with a majority of delegates, then you can guarantee that that candidate will win this kind of competition. Even if every other candidate's delegates teamed up to knock down the delegates of the candidate with the majority, there wouldn't be enough.

It then proceeds to develop a sequential algorithm that simulates with kind of voting scheme. You keep two variables, *K* and *CAND*. Initialize *K* to 0. Then you visit each delegate in turn. When *K* is 0, you set *CAND* to the next delegate you visit and set *K* to 1. When *K* is greater than 1, you increment *K* by 1 if the next delegate is equal to *CAND* and decrement *K* by 1 if it is not equal to *CAND*.

In this way, you are able to pair each delegate with a delegate you previously saw. This algorithm takes advantage of the fact that while performing this process, if there is ever a prefix of the sequence where exactly half of the delegates are for one candidate, and the other half is for other candidates, then you can chop off this prefix and the solution to the overall problem will remain the same.

If you're performing this algorithm on a stream of data and you're unsure whether it has a majority, you can use this algorithm to come up with a candidate for the majority. At the end, you can scan through the stream again and just count the number of elements for that candidates and the number of total elements. Thus you can use this algorithm to find the majority if it exists or know that there isn't a majority, all in *O(n)* time and *O(1)* memory.