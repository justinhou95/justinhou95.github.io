---
layout:     post
title:      Artificial Neural Networks
subtitle:   
date:       2019-02-15
author:     Songyan Hou
header-img: img/404-bg.jpg
abstract: In this article, we give an introduction of the structures of artificial neural networks(ANNs), especially the rectified ANNs with analysis on operations between ANNs and show some concrete examples of ANNs.
catalog: true
tags:
    - ANNs
---
Artificial Neural network is a significant function structure which has the capacity to realize a board range of functions and plays an important role in machine learning algorithm and function approximating theory. Application areas of ANNs include vehicle control, decision making, pattern recognition, medical diagnosis, financial applications, data mining and filtering problems. So in this blog, we would like to introduce the structure of ANNs and give some concrete examples.
# 1. Structure of ANNs
An artificial neural network is a structure to produce a function which is alternately compositions of affine linear transformations and activation functions. We should keep in mind that ANN is nothing other than a structure or a graph and the function produced by it is called the realization of this ANN.

$$ \mathcal{N} = \Psi_{L} \circ \mathcal{A}_{l_{L},l_{L-1}} \circ \Psi_{L-1} \circ \mathcal{A}_{l_{L-1},l_{L-2}}\cdots \Psi_{1} \circ \mathcal{A}_{l_{1},l_{0}}$$

where $\Psi_{k}\colon \mathbb{R}^{l_{k}} \to \mathbb{R}^{l_{k}}, k=1,\cdots,L$ is a function on $\mathbb{R}^{l_{k}}$ (called the activation functions) and $$\mathcal{A}_{l_{k},l_{k-1}}\colon \mathbb{R}^{l_{k-1}} \to \mathbb{R}^{l_{k}}, k=1,\cdots,L$$ is affine linear transformation from $\mathbb{R}^{l_{k-1}}$ to $\mathbb{R}^{l_{k}}$. Explicitly, we write for all $$x\in \mathbb{R}^{l_{k-1}}$$ that 

$$\mathcal{A}_{l_{k},l_{k-1}}(x) = W_{k}x + B_{k}$$

where $W_{k} \in \mathbb{R}^{l_{k}\times l_{k-1}}$ (called weight) and $B_{k} \in \mathbb{R}^{l_{k}}$ (called Bias)
![My helpful screenshot](/img/ANN/ANN1.png)
Here are 3 important index related to a ANN namely which are degree, layers and realization. Let $\phi$ be a ANN inheriting the structure and notation above.


### Degree 
the degree of $\phi$ is the dimension of memory to store all the affine linear transformation given by 

$$\mathcal{P}(\phi) = \sum_{k=1}^{L}l_{k}(l_{k-1}+1)$$

### Layer
the layer of $\phi$ is the vector of the dimension of all layers defined by

$$\mathcal{L}(\phi) = (l_{0},\cdots,l_{L})$$

### Realization
the realization of $\phi$ is the function you get from the ANN structure $$\mathcal{R}(\phi)\colon \mathbb{R}^{l_{0}} \to \mathbb{R}^{l_{L}}$$ defined by 

$$\mathcal{R}(\phi)(x) = \mathcal{N}(x) = \Psi_{L} \circ \mathcal{A}_{l_{L},l_{L-1}} \circ \Psi_{L-1} \circ \mathcal{A}_{l_{L-1},l_{L-2}}\cdots \Psi_{1} \circ \mathcal{A}_{l_{1},l_{0}}(x)$$

# 2. Activation functions
In general, activation functions $$\Psi_{k}$$ can be different functions in one ANN and they endow the ANN the nonlinear behavior. So now we started to introduce an important class of activation functions, namely the multidimensional versions.
### Rectifier function
Bionic idea from real neural network of human being gives a natural activation functions called the rectifier function

$$r(x) = \max\{x,0\}$$

### Heaviside function
Heaviside function given by

$$h(x) = 1_{[0,\infty)}$$

### Standard logistic function
Standard logistic function is given by

$$l(x) = \frac{1}{1+\exp(-x)}$$

which act as a smooth approximation of the Heaviside function.
![My helpful screenshot](/img/ANN/ANN2.png)
### Softplus function
Softplus function is given by

$$s(x) = \ln(1+\exp(x)) = \int_{-\infty}^{x}l(t)dt$$

which act as a smooth approximation of the rectifier function. 
![My helpful screenshot](/img/ANN/ANN3.png)
Also notice that 

$$s(x) = \int_{-\infty}^{x}l(t)dt$$

$$r(x) = \int_{-\infty}^{x}h(t)dt$$

### Multidimensional version
Since the activation function introduced above are from $\mathbb{R}$ to $\mathbb{R}$, we need a multidimensional version in order to use them under any dimension. The multidimensional version of a function $\phi\colon \mathbb{R} \to \mathbb{R}$ denoted by $$m_{\phi,d}\colon \mathbb{R}^{d} \to \mathbb{R}^{d}$$ is defined by

$$m_{\phi,d}(x_{1},\cdots,x_{d}) = (\phi(x_{1}),\cdots,\phi(x_{d}))$$
Sometimes we are interested in the ANN where all activation functions but the last one are a multidimensional version of the same real valued nonlinear function and the last one is the identity function because this model is sufficient to solve the problem. We call this simple ANN and call $\phi$ the basis activation function of this simple ANN. The following is an intuitive structure graph of the simple ANN.
![My helpful screenshot](/img/ANN/ANN4.png)

# 3. Operations of ANNs
## 3.1. Sums of ANNs with the same structure
Assume we have $M$ many simple ANN $\phi_{m}$ with the same structure i.e. same $l_{0},\cdots l_{L}$ and same basis activation function $a$.
![My helpful screenshot](/img/ANN/ANN5.png)
We hope to construct a DNN $\psi$ use less degree and satisfies that 

$$\mathcal{R}(\psi) = \sum_{m=1}^{M}h_{m}\mathcal{R}(\phi)$$

and this can be obtain by introducing the following ANN 
![My helpful screenshot](/img/ANN/ANN6.png)
and the it satisfies that 

$$\mathcal{P}(\psi) \leq M^{2}\mathcal{P}(\phi_{1})$$

## 3.2. Composition of ANNs
Given $\phi_{1}$ and $\phi_{2}$ two simple DNN such that $\mathcal{R}(\phi_{1}) \in C(\mathbb{R}^{d_{2}},\mathbb{R}^{d_{3}})$ and $\mathcal{R}(\phi_{2}) \in C(\mathbb{R}^{d_{1}},\mathbb{R}^{d_{2}})$. 
![My helpful screenshot](/img/ANN/ANN7.png)
![My helpful screenshot](/img/ANN/ANN8.png)
We hope to define a $\psi$ with less degree such that 

$$\mathcal{R}(\psi) = \mathcal{R}(\phi_{1}) \circ \mathcal{R}(\phi_{2})$$

A natural idea is to construct a following DNN 
![My helpful screenshot](/img/ANN/ANN9.png)
However this is not a simple DNN because the green identity function in the middle does not belong to the same multidimensional version activation functions class as the red ones. So we first think of that we should delete the bothering layer after the green identity function in the middle. Thus we come to the following structure
 ![My helpful screenshot](/img/ANN/ANN10.png)
 This solves the problem. However, in practice $d_{2}$ is usually greatly smaller than the dimension of layers so there is a smarter way avoid making the degree so high. Let $I$ be a DNN with layer $(d_{2},i,d_{2})$ (usually $i$ is as small as $d_{2}$ and $i=2d_{2}$ in the case of rectifier ANN) and the realization of $I$ is the identity function. We introduce the following structure 
  ![My helpful screenshot](/img/ANN/ANN11.png)
  If we compute the difference of degree between $\psi$ and $\tilde{\psi}$ we have 
  
  $$
  \begin{align*}
    \mathcal{P}(\tilde{\psi}) - \mathcal{P}(\mathcal{\psi}) &= l_{1,1}(l_{2,L_{2}-1}+1) - i(l_{2,L_{2}-1}+1) - l_{1,1}(i+1)\\
    &= l_{1,1}l_{2,L_{2}-1} - i(l_{1,1}+l_{2,L_{2}-1}) -i\\
    &= l_{1,1}l_{2,L_{2}-1} - i(l_{1,1}+l_{2,L_{2}-1}+1)\\
    &\geq l_{1,1}l_{2,L_{2}-1} - i(l_{1,1}+l_{2,L_{2}-1}+i)\\
  \end{align*}
  $$

  Assume there exists k such that $$ki \leq \min\{l_{1,1},l_{2,L_{2}-1}\} \leq \max\{l_{1,1},l_{2,L_{2}-1}\} \leq 2ki$$ where $k \geq 5$. Then er asdasda 

  ## 1. asdad
  sakjdslkskdkjkllsadjsadlajjjjjjjjjjjjj

    $$
  \begin{align*}
    \mathcal{P}(\tilde{\psi}) - \mathcal{P}(\mathcal{\psi}) &\geq l_{1,1}l_{2,L_{2}-1} - i(l_{1,1}+l_{2,L_{2}-1}+i)\\
    &\geq k^2i^2 - i(4ki+i)\\
    &\geq i^2(k^2 - 4k -1) \\
    &\geq 4i^2 \\
  \end{align*}
  $$
