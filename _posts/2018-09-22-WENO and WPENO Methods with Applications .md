---
layout:     post
title:      WENO and WPENO Methods with Applications
subtitle:   
date:       2018-09-22
author:     Songyan Hou
header-img: img/fd.jpg
abstract: In this article we discuess two extension of essentially non-oscillatory methods, WENO method and WPENO method with their applications on conservation law. Both ofthem are designed to obtain high order of accuracy meanwhile maintaining the shock capturing features mainly for convection dominating equations. 
catalog: true
tags:
    - WENO
    - Numerical method
---

## Introduction
In this paper we discuss two extension of essentially non-oscillatory methods, WENO method and WPENO method with their applications on conservation law. Both of them are designed to obtain high order of accuracy meanwhile maintaining the shock capturing features mainly for convection dominating equations. Particularly, the WPENO method, based on an extended class of limiters substantially reduces the discontinuity smearing feature which lots of other schemes show in numerical experiments. We construct the fifth-order WENO method as well as the fifth-order WPENO method in two different ways, cell-averaging and flux-averaging. Furthermore, We discuss the difference and show the algorithm of both reconstruction procedure separately in our numerical experiments. Additionally, the artificial flux sharpening technique as well as the shock locating technique are introduced to both methods to reduce the discontinuity smearing features and unnecessary use of limiters . We present several numerical experiments including scalar and systems of conservation laws including linear advection, burgers' equations and euler systems of gas dynamics and compare the numerical performance both on smooth regions and the fierce ones.
## Slides
[Slides could be found here](/documents/WENO.pdf)

![My helpful screenshot](/img/WENO and WPENO Methods with Applications/weno_ppt.png)