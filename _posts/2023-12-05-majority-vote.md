---
layout: post
title:  "The Boyer–Moore Majority Vote Algorithm"
date:   2023-12-05
categories: [algorithms]
permalink: majority-vote
description: "The Boyer–Moore majority vote algorithm"
---

Let's say you have a stream of elements of unbounded size. You know that one element appears a majority of the time. Can you find that majority element in a single scan using constant memory? There's an interesting algorithm to do this called the [Boyer–Moore majority vote algorithm](https://doi.org/10.1007/978-94-011-3488-0_5).

The paper describes the idea behind the algorithm using the analogy of a convention center filled with delegates for a number of political candidates. We imagine that "voting" happens like this: delegates can knock each other down to cancel out the vote of another delegate, however the knocker also gets knocked down too. The candidate with the last delegate(s) standing wins. If there is a candidate with a majority of delegates, you can guarantee that that candidate will win this kind of competition. Even if every other candidate's delegates teamed up to knock down the delegates of the candidate with the majority, there wouldn't be enough.

It then proceeds to develop a sequential algorithm that simulates this voting scheme. You keep two variables, *K* and *CAND*. Initialize *K* to 0. Then visit each delegate in turn. When *K* is 0, set *CAND* to the current delegate and increment *K*. When *K* is greater than 1, then increment *K* by 1 if the current delegate is equal to *CAND*, and decrement *K* by 1 if not.

In this way, you are able to pair each delegate for every candidate but one with a delegate for another candidate that you previously saw: the delegate that causes you to increment *K* gets paired with the delegate that causes you to decrement *K* later. If *K* is greater than 1 after processing the last delegate, then there are *K* unpaired delegates for *CAND*. This algorithm takes advantage of the fact that while performing this process, if there is ever a prefix of the sequence where exactly half of the delegates are for one candidate, and the other half is for other candidates, then you can chop off this prefix and the solution to the overall problem will remain the same. Therefore, the *K* unpaired delegates for *CAND* indicates that only *CAND* can possibly have a majority, if there is one.

If you're performing this algorithm on a stream of data and you're unsure whether it has a majority, you can use this algorithm to come up with a candidate for the majority. At the end, you can scan through the stream again counting both the candidate elements and total elements. If the candidate elements are a majority, you have as solution. If not, there is no majority. All this can be done in in *O(n)* time and *O(1)* memory for a stream of unbounded size.