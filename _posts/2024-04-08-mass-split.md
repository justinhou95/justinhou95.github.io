---
layout: post
title: Mass splitting under adapted Wasserstein distance
date: 2024-04-08 11:12:00-0400
description: 
tags: 
categories:
related_posts: false
---

In classical optimal transport, simply by Jensen's inequality we have

$$
\mathcal{W}_1(\frac{1}{N}\sum_{n=1}^N \mu_n, \frac{1}{N}\sum_{n=1}^N \nu_n) \leq \frac{1}{N}\sum_{n=1}^N \mathcal{W}_1(\mu_n, \nu_n).
$$

However in adapted optimal transport, this is in general not true. A simple counter example is by taking $$\mu_1 = \delta_{(0,1)}$$, $$\mu_2 = \delta_{(0,-1)}$$, $$\nu_1 = \delta_{(\varepsilon,1)}$$, $$\nu_2 = \delta_{(-\varepsilon,-1)}$$. Then we have 

$$
\mathcal{AW}_1(\frac{1}{N}\sum_{n=1}^N \mu_n, \frac{1}{N}\sum_{n=1}^N \nu_n)  = 1-\varepsilon > \varepsilon = \frac{1}{N}\sum_{n=1}^N \mathcal{AW}_1(\mu_n, \nu_n).
$$

Conjecture: under some regularity conditions (quantified by $$\epsilon$$), we have 

$$
\mathcal{AW}_1(\frac{1}{N}\sum_{n=1}^N \mu_n, \frac{1}{N}\sum_{n=1}^N \nu_n) \leq \frac{1}{N}\sum_{n=1}^N \mathcal{AW}_1(\mu_n, \nu_n) + C_\epsilon.
$$







