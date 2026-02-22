---
layout: post
title: When causal and classical Wasserstein are equivalent
date: 2026-02-22 11:12:00-0400
description: 
tags: 
categories:
related_posts: false
---

**Notation** We denote by $$\mathbf{S} \subset \mathbb{R}^{T\times T}$$ the set of symmetric matrices, $$\mathbf{S}_+ \subset \mathbb{R}^{T\times T}$$ the set of symmetric positive semi-definite matrices, $$\mathbf{L}\subset \mathbb{R}^{T\times T}$$ the set of lower triangular matrices, $$\mathbf{L}_+\subset \mathbb{R}^{T\times T}$$ the set of lower triangular matrices with non-negative diagonal, $$\mathbf{D}\subset \mathbb{R}^{T\times T}$$ the set of diagonal matrices, $$\mathbf{O}\subset \mathbb{R}^{T\times T}$$ the set of orthogonal matrices. We denote by $$\|\cdot \|_2$$ the operator norm and $$\|\cdot\|_{\mathrm{F}}$$ the Frobenius norm. The condition number of a matrix $$A$$ is $$\kappa_2(A) = \| A^{-1}\|_2 \|A\|_2$$.

---

### Adapted Wasserstein distance

The adapted Wasserstein distance is introduced as a strengthend version of classical Wasserstein distance by incorporating the temporal causal structure in order to guarantee robustness of stochastics optimization problem. Recall classcial Wasserstein distance $$\mathcal{W}_2$$ is defined via

$$
\mathcal{W}_2^2(\mu,\nu) = \inf_{(X,Y) \sim (\mu,\nu)} \mathbf{E}[|X - Y|^2],
$$

while the adapted Wasserstein distance $$\mathcal{AW}_2$$ (with nested representation) is defined via 

$$
\mathcal{AW}_2(\mu,\nu) = \inf_{(X,Y) \sim_{\rm bc} (\mu,\nu)} \mathbf{E}^{1/2}[|X - Y|^2],
$$

where $$\sim_{\rm bc}$$ imposes addition bicausal restriction on $$(X,Y) \sim (\mu,\nu)$$, so trivially $$\mathcal{W}_2\leq \mathcal{AW}_2$$. This bicausal restriction enforces non-anticipativity in both directions and thus provide a natural and robust framework for stochastic optimization problems i.e. for many optimal values of stochastic optimization problem $$\mathcal{V}(\mu)$$ we have 

$$
|\mathcal{V}(\mu) - \mathcal{V}(\nu)| \lesssim \mathcal{AW}_2(\mu,\nu)
$$

but this does not hold for $$\mathcal{W}_2$$. 

### Gaussian processes 
For Gaussian processes, both $$\mathcal{W}_2$$ and $$\mathcal{AW}_2$$ have closed-form solutions. For simplicity we consider centered real-valued Gaussian process. 

Then $$\mathcal{W}_2$$ is given by

$$
\mathcal{W}_2^2(\mu,\nu) = \min_{O\in\mathbf{O}}\Vert A^{1/2} - B^{1/2}O\Vert_2^2 =: d_{\rm BW}^2(A,B),
$$

and $$\mathcal{AW}_2$$ is given by 

$$
\mathcal{AW}_2^2(\mu,\nu) = \min_{D\in\mathbf{D}\cap \mathbf{O}}\Vert L - MO \Vert_2^2 =: d_{\rm ABW}^2(L,M),
$$

where $$A,B$$ are covairance matrices of $$\mu,\nu$$ and $$A = LL^\top$$, $$B = MM^\top$$ are Cholesky decomposition with non-negative diagonals. 


### When causal and non-causal distances are equivalent?
It is not difficult to construct examples when $$ \mathcal{W}_2(\mu,\nu) \to 0$$ while $$\mathcal{AW}_2(\mu,\nu)$$ is large, so $$\mathcal{W}_2$$ and $$\mathcal{AW}_2$$ can not be equivalent in general (they induce different topology). However, in Gaussian case, it turns out that in a ball around regular Gaussian process, they are actually equivalent i.e. there exists $$C > 0$$ such that for all $$\mu, \nu$$ in the ball

$$
\mathcal{W}_2(\mu,\nu) \leq \mathcal{AW}_2(\mu,\nu) \leq C\cdot \mathcal{W}_2(\mu,\nu).
$$

Let $$A \in \mathbf{S}_+$$, and $$LL^\top = A$$ be the Cholesky decomposition where $$L \in \mathbf{L}_+$$. For a small perturbation $$\Delta A \in \mathbf{S}$$, let $$(L+\Delta L)(L + \Delta L)^\top = A + \Delta A$$ be the Cholesky decomposition where $$\Delta L \in \mathbf{L}$$. By the stability result of Cholesky decomposition; see [1], we know that if $$\|\Delta A\|_{\mathrm{F}} < \frac{1}{2\| A^{-1}\|_2}$$, then the Cholesky decomposition of $$A+\Delta A$$ is unique and 

$$
\|\Delta L\|_F \leq (2 + \sqrt{2})\| A^{-1}\|_2\| A\|_2^{1/2}\|\Delta A\|_{\mathrm{F}}.
\tag{1}
$$

Now, denote $$B = A + \Delta A$$ and $$M = L + \Delta L$$. Note that for all $$O \in \mathbf{O}$$, we have

$$
\begin{aligned}
\|A - B\|_\mathrm{F}
&\leq \| A^{\frac{1}{2}} A^{\frac{1}{2}} - A^{\frac{1}{2}}OB^{\frac{1}{2}} + A^{\frac{1}{2}}OB^{\frac{1}{2}} - B^{\frac{1}{2}}B^{\frac{1}{2}}\|_2 \\
&\leq \| A^{\frac{1}{2}} \|_2 \| A^{\frac{1}{2}} - OB^{\frac{1}{2}}\|_\mathrm{F}
+ \| O B^{\frac{1}{2}} \|_2 \|A^{\frac{1}{2}} - B^{\frac{1}{2}} O^\top\|_\mathrm{F}\\
& \leq (\| A^{\frac{1}{2}} \|_2 + \| B^{\frac{1}{2}} \|_2) \|A^{\frac{1}{2}} - B^{\frac{1}{2}} O^\top\|_\mathrm{F}.
\end{aligned}
$$

Taking the minimum over all $$O \in \mathbf{O}$$ yields that

$$
\|\Delta A\|_\mathrm{F} \leq (\| A^\frac{1}{2}\|_2 + \| B^\frac{1}{2}\|_2) d_{\rm BW}(A,B).
$$

Plugging this estimate to (1), we obtain

$$
d_{\rm ABW}(L,M) \leq (2 + \sqrt{2})\| A^{-1}\|_2\| A\|_2^{1/2}\| (\| A^\frac{1}{2}\|_2 + \| B^\frac{1}{2}\|_2) d_{\rm BW}(A,B).
$$

Let $$(A_t)_{t\in [0,1]}$$ be a geodesic on $$(\mathbf{S}_{+},d_{\rm BW})$$ connecting $$A$$ to $$B$$, then

$$
d_{\rm ABW}(L,M) \leq \left(\int_0^1 2(2 + \sqrt{2})\| A_t^{-1}\|_2\| A_t\|_2^{1/2}\| \| A_t^\frac{1}{2}\|_2  dt\right)d_{\rm BW}(A,B).
$$

Therefore, on a geodesically convex set where $$\| A^{-1}\|_2\| A\|_2^{1/2}\| \| A^\frac{1}{2}\|_2$$ upper-bounded, the following equivalence holds:

$$
d_{\rm ABW}(L,M) \leq C\cdot d_{\rm BW}(A,B).
$$

### Discussion

The take home message is: if you’re working on distributional robustness around a regular Gaussian processes, causal and non-causal distances are equivalent, so just pick one you like. 

A natural next question is whether this could be extended to more general cases. Extending to multi-dimensional Gaussian processes case I believe is quite manageable. Extending this to general ``regular" stochastic processes is a bit more subtle. To me, there are at least two challenging questions to answer. First, what is the right characterization of regularity? Second, how can one estimate distances without the privilege closed-form solutions? If you are also interested in this and have an idea, feel free to reach me out. If you worry that this would make the study of causal distance useless, also reach me out and I am also happy to chat about that.

----------

### Reference
[1] X-W Chang and Damien Stehl´e. “Rigorous perturbation bounds of some matrix factorizations”. SIAM journal on matrix analysis and applications 31.5 (2010), pp. 2841–2859.