---
layout: post
title:  "Fail Open and Fail Closed"
date:   2023-11-30
categories: [engineering]
permalink: fail-open-closed
description: "Fail Open and Fail Closed"
---

I was reading about rate limiters today, and the issue of behavior under failure came up. There are two main failure modes: fail open and fail closed. These terms seem like intuitive ways of describing how traffic flows during a rate limiter failure: either it flows or it doesn't. And it's not hard to figure out what term means what, right?

Well that's what I thought. It seemed to me like *fail open* should mean that traffic *doesn't flow* during a failure---like an open circuit. And *fail closed* should mean that traffic *flows* during a failure---like a short circuit. But the terms were actually being used to mean the opposite: *fail open* means that traffic *flows*, and *fail closed* means that it *doesn't flow*. I thought that this must be a mistake, since I originally learned these terms in the context of circuits and I assumed that's where they came from. However, some Googling lead me to realize that when designing valves, the opposite terminology is used: *fail open* means that the valve is open, and allows fluid to flow, *fail closed* means that the valve is closed, and doesn't allow fluid to flow.

So what's the right terminology to use? Well I guess it depends on whether you think that internet traffic is more like a fluid through a pipe or electricity through a wire. Of course, internet traffic literally *is* electricity through a wire (or light through a fiber), but a fluid is an easier metaphor to understand. On the other hand, software engineers are probably more likely to have a background in electronics than hydraulics, so it's hard to say. Sometimes obvious things aren't so obvious!