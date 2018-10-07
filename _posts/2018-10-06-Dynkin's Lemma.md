---
layout:     post
title:      Dynkin's Lemma with Applications
subtitle:   
date:       2018-09-22
author:     Songyan Hou
header-img: img/Dynkin.jpg
abstract: In this article we introduce Dynkin's Lemma with their application. In Dynkin's Lemma used proof, we define a so called Dynkin's property have an insight of what difficulty does Dynkin's Lemma really helps to overcome and under what condition Dynkin's lemma really help. Besides the use of a Dynkin's property language shorten the proof without repeating programized arguments of using Dynkin's Lemma.
catalog: true
tags:
    - Probability Theory
---
# Dynkin's Lemma with Applications

## Introduction

Dynkin's Lemma, also called Dynkin's $$\pi$$ Lemma, named by Eugene Dynkin, characterizes the situation when a Dynkin's property is already valid on a $$\pi$$-system, usually chosen to be generator of a desired $$\sigma$$-algebra. Under this condition, the property is also true on a $$\sigma$$-algebra which usually be the collection measuable sets $$\mathcal{F}$$ on a probability space$$(\Omega,\mathcal{F},P)$$

## Dynkin's lemma

![My helpful screenshot](/img/Dynkin_lemma.png)

## Dynkin's property

Here we define Dynlin's property in a slightly general way $$i.e.$$ $$X$$-property where X can be any system, such as $$\sigma$$-system, Dynkin system or $$\pi$$-system.
![My helpful screenshot](/img/Dynkin_property.png)

In fact, Dynkin corollory here is nothing other than a restatement of Dynkin's lemma, in which the Dynkin system is a system of set which satisfis certain property. However in the next section, we will the convenience and insight of this restatement.

## Application to the probability theory

First, let us see some examples of Dynkin properties in the probability theory.

### Examples of Dynkin's property

![My helpful screenshot](/img/Dynkin_example.png)

It can be easily check that those are Dynkin properties. So, by the Dynkin's corollary above, if we want such property in a $$\sigma$$-system, the only work is to find a $$\pi$$-system, sets on which satisfies this property and after that, the proof will be done by Dynkin's corollary automatically. Now let's see the power of Dynkin's corollary.

### Power of Dynkin's corollary

#### 1. proof of the independence formula
![My helpful screenshot](/img/Dynkin_power2.png)

#### 2. proof of the equality of two measure
![My helpful screenshot](/img/Dynkin_power1.png)

#### 3. proof of the uniqueness of the measure
![My helpful screenshot](/img/Dynkin_power3.png)
![My helpful screenshot](/img/Dynkin_power4.png)

### Conclusion
Dynkin's corollary transfer the original Dynkin property problem to finding a $$\pi$$-system to satisfy the Dynkin property. Usually the $$\pi$$-system is directly from the most necessary and corest condition of the theorem. Besides these two examples, if you find more Dynkin property with any interesting and essential theorem related to it, please tell me so that I can add a new power of Dynkin's corollary. The inspiration of this article arise from the class of The Probability taught by Prof. Dr. Alain-Sol Sznitman in Fall Semester 2018 in ETH, whom I really appreciate for excellent teaching.  

### Appendix
![My helpful screenshot](/img/Dynkin_appendix0.png)
![My helpful screenshot](/img/Dynkin_appendix1.png)
![My helpful screenshot](/img/Dynkin_appendix2.png)

### Reference

- [Dynkin System Wikipedia](https://en.wikipedia.org/wiki/Dynkin_system)
- [Lecture notes of Probability Theory by Prof. Dr. Alain-Sol Sznitman]( )


