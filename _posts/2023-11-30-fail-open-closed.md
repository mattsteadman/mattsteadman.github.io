---
layout: post
title:  "Fail Open and Fail Closed"
date:   2023-11-30
categories: [engineering]
permalink: fail-open-closed
description: "Fail Open and Fail Closed"
---

I was reading about rate limiters today, and the issue of how it should behave under failure came up. There are two main failure modes to consider: fail open and fail closed. Most people will read these two terms and immediately know what they refer to: the issue of whether traffic flows during a failure of the rate limiter. And obviously, it's not hard to figure out which term refers to which mode, right?

Well that's what I thought. Of course, fail open means that traffic doesn't flow during a failure---like an open circuit---and fail closed means that fail closed means that traffic flows during a failure---like a short circuit. But according to what I was reading, it's actually the opposite: fail open means that traffic flows, and fail closed means that it doesn't flow. I thought that this must be a mistake, until some Googling lead me to realize that when designing valves, the opposite terminology is used. Fail open means that the valve is open, and allows flow. While fail closed means that the valve is closed, and doesn't allow flow.

So what's the right terminology to use? Well maybe it depends on whether you think that internet traffic is more like a fluid through a pipe or electricity through a wire. Of course, internet traffic literally **is* electricity through a wire (or light through a fiber), but a fluid is an easier metaphor to understand. On the other hand, software engineers are probably more likely to have a background in electronics than fluid mechanics, so it's hard to say. I guess the real lesson is, don't assume you know which is which without asking!