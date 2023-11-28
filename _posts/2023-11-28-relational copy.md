---
layout: post
title:  "The Many Parameters of Op-Amps"
date:   2023-11-28
categories: [electronics]
permalink: op-amps
description: "The Many Parameters of Op-Amps"
---

When I was first learning about electronics, one of the things I remember being fascinated by was the many ways in which op-amps could vary. In their ideal form, op-amps seem like such pretty simple devices: they amplify the difference between their two inputs. But in practice, this turns out to be a very leaky abstraction. There are many assumptions about the ideal op-amp that never hold in practice:
- _Open-loop gain:_ It turns out that in practice it's hard to build an op-amp with infinite gain, but many real op-amps have reasonably large gains. In either case, it rarely matters because you're using an op-amp in a closed-loop configuration.
- *Input impedance:* Because of the capacitive coupling inherent to the design of MOSFETs (not to mention leakage current), it turns out that assuming you have infinite input impedance is unrealistic.
- __Output impedance:__ Similarly, the output of an op-amp isn't a perfect voltage source and has some amount of output impedance.
- **Input offset voltage:** It turns out that the input voltage that produces an output of 0 V isn't actually 0 V, there's always some voltage difference needed to actually get to 0.
- **Input current:** Because of leakage current of your MOSFETs, a certain amount of current will flow into your inputs. It's assumed to be zero, but it's not.
- **Common-mode rejection ratio:** We assume that a signal that appears equally on both input will produce no output, but actually the ability of an op-amp to reject common signals varies. This is measured by a parameter called common-mode rejection ratio (CMRR).
- **Power-supply rejection ratio:** Similarly, a signal that appears on the power supply shouldn't make it to the output, but in practice op-amps have finite power-supply rejection ratios (PSRR).
- **Slew rate:** This is the parameter that I remember first made me ask the question "How many different parameters are there to an op-amp anyway?" This is the speed at which the output of an op-amp can change ("slew"). In other words, when the output of your op-amp should be a square wave, the slope of the lines will actually be less than infinite. The slew rate is that slope.
- **Gain–bandwidth product:** Real op-amps have finite bandwidth. The bandwidth turns out to be a function of gain. However, the product of gain and bandwidth turns out to be independent of frequency. This parameter is called gain–bandwidth product (GBWP).
- **Noise:** For some applications, like audio, low-noise output is important, and so you can find op-amp specifically designed to be low-noise.
- **Output voltage:** It's to be expected that the output voltage will saturate at the power supply voltage, but unless your op-amp is specifically designed to be rail-to-rail, it will saturate at a value less than that.
- **Output current:** Op-amps can only source (and sink) so much current from their output.