---
layout:     post
title:      Generators of random variables 
subtitle:   
date:       2018-12-25
author:     Songyan Hou
header-img: img/tc.jpg
abstract: In this article, we briefly introduce some generators of random variables and present the realization detail of some simple but commonly used distribution and attach the Matlab codes.

catalog: true
tags:
    - Probability theory
    - Numerical method
---
In this article, we briefly summarize some generators of random variables introduced in the Notes of Numerical Analysis of Stochastic Differential Equations by Prof. Dr. Arnulf Jentzen and present the realization detail of some simple but commonly used distribution and attach the Matlab codes, most of which also come from the lecture note. This article act as a short summary of the content concerning on the generation of random variable in the lecture note.
# 1. Generation of Random Variables
Before answering the question how to generate an arbitrary random variable, a natural question is how to generate a Bernoulli distributed random variable? Tossing a coin is a good idea. In fact, there are numbers of random number generator based on certain physical experiments but for a general distributed random variable, the physical experiments may not be designed easily or might not realize efficiently. This can be one of the motivation of developing methods to generate random variable in a boarder stage with the elementary ones such as Bernoulli distributed denoted by $$\text{Ber}_{p}$$ or uniformly $$(0,1)$$ distributed denoted by $$\mathcal{U}_{(0,1)}$$ random variables. Because of the limitation of constructing continuous distribution with $$\text{Ber}_{p}$$-distributed random variables, through this article we assume that we have a black box which can generate independent $$\mathcal{U}_{(0,1)}$$-distributed random variables as many as we want.
# 2. A Brief Introduction of Methods
In this first section we briefly introduce three types of generators of random variables. The introduction of methods all follow from the Lecture notes of Numerical Analysis of Stochastic Differential Equations by Prof. Dr. Arnulf Jentzen. Firstly, we present the inversion method which is a method accessible for general one dimensional distribution with explicit distribution function. Secondly, we introduce the acceptance-rejection method which helps to generate a uniform distribution on a complicated bounded domain. Also we focus on the application of the acceptance-rejection method on generate general multi-dimensional distribution with explicit density. Lastly, we present two methods: the Box-Muller method and the Masaglia method, which are designed for standard normal distribution based on the polar representation of the normal distribution. Furthermore, we discuss how to obtain a general normal distributed random variable by imposing a affine linear transformation on the standard one.
## 2.1. Inversion method
Loosely speaking and in discrete situation, the basic idea of the inversion method is to cut the $$(0,1)$$ interval into pieces and assign each piece with a certain value. The partition and values are chosen such that the length of the piece with certain value is exactly the probability when the desired random variable hit such value.
![My helpful screenshot](/img/Generation of random variables/Generators of random variables 1.png)
![My helpful screenshot](/img/Generation of random variables/df.png)
![My helpful screenshot](/img/Generation of random variables/Generators of random variables 2.png)
## 2.2. Acceptance-Rejection method
Like it's name, the acceptance-rejection method is an 'algorithm' only acceptance events that we want. By acceptance and rejection, we can generate a uniformly distributed random variable on a complicate domain from the uniformly distributed random variable on a larger but more regular domain. This observation with the connection between subgraph of unnormalized density function with distribution gives a way to realize a random variable with explicit density function.
![My helpful screenshot](/img/Generation of random variables/mc.png)
![My helpful screenshot](/img/Generation of random variables/Generators of random variables 3.png)
![My helpful screenshot](/img/Generation of random variables/Generators of random variables 4.png)
MultivariateNormal
## 2.3. Methods for Normal distribution
Because of the significance of normal distribution in many application of statistic and stochastic stimulation, several methods specific for normal distribution are introduced. A direct use of the central limit theorem gives the normal distribution. But considering it's a limit algorithm requires many copies of i.i.d. random variables, we introduce another way of constructing the normal distribution which use the polar representation of $$2$$-dimensional normal distribution. We firstly present the method only for standard normal distribution and later construct the general one by affine linear transformation. 
![My helpful screenshot](/img/Generation of random variables/MultivariateNormal.png)
![My helpful screenshot](/img/Generation of random variables/Generators of random variables 5.png)
![My helpful screenshot](/img/Generation of random variables/Generators of random variables 6.png)
# 3. Matlab Code and Realization
In this section we present how to realize some simple distribution in practice.In our matlab realization, we use the pseudo random number generator function by default in matlab which gives a sequence of realization of pseudo random numbers which is not a sequence of real random numbers but gives the same statistic property and can be reproduced.
## 3.1. Inversion method
There are usually two steps in the inversion method. Firstly, compute the general inverse distribution function. Secondly, composite it with a $\mathcal{U}_{(0,1)}$-distributed random variable.
### Exponential distribution
```matlab
function [X] = rand_exp(lambda,N)
U = rand(1,N);
X = -log( U )/lambda;
end
 ```
 ![My helpful screenshot](/img/Generation of random variables/Generators of random variables c1.png)
### Cauchy distribution
```matlab
function [X] = rand_cauchy(mu,lambda,N)
U = rand(1,N);
X = lambda * tan(pi*(U - 0.5)) + mu;
end
 ```
  ![My helpful screenshot](/img/Generation of random variables/Generators of random variables c2.png)
### Laplace distribution
```matlab
function [X] = rand_laplace(lambda,N)
U = rand(1,N);
X = ( log( 2 * U )/lambda .* (U <= 0.5) - log( 2 * (1 - U) ) .* (U > 0.5) ) / lambda;
end
 ```
  ![My helpful screenshot](/img/Generation of random variables/Generators of random variables c3.png)
### Bernoulli distribution
Although to generate a Bernoulli distribution with the uniform distribution is not how it works in practice but here we present it as an example of using the inverse method.
```matlab
function [X] = rand_ber(p,N) 
U = rand(1,N);   % generate uniformly distributed random variable
X = U > (1-p);   % general inverse distribution function
end
 ```
![My helpful screenshot](/img/Generation of random variables/Generators of random variables d1.png)
### Binomial distribution
```matlab
function [X] = rand_bi(p,n,N)
X = zeros(1,N);
amp_c = p/(1-p);
p_initial = (1-p)^n;
for it = 1:N
    k = 0;
    u = rand(1,1);
    p_single = p_initial;
    threshold = p_initial;
    while u > threshold
        amp = amp_c * (n-k) / (k+1);
        p_single = p_single * amp;
        threshold = threshold + p_single; 
        k = k+1;
    end
    X(it) = k;
end
end
 ```
   ![My helpful screenshot](/img/Generation of random variables/Generators of random variables d2.png)
### Geometric distribution
```matlab
function [X] = rand_geom(p,N)
U = rand(1,N);
X = floor(log(U) / log(1-p) );
end
 ```
![My helpful screenshot](/img/Generation of random variables/Generators of random variables d3.png)
### Shifted-geometric distribution
```matlab
function [X] = rand_sgeom(p,N)
U = rand(1,N);
X = floor(log(U) / log(1-p) );
X = X+1;
end
 ```
![My helpful screenshot](/img/Generation of random variables/Generators of random variables d4.png)
### Poisson distribution
```matlab
function [X] = rand_poi(lambda,N)
expo = 2.71828;
X = zeros(1,N);
amp_c = lambda;
p_initial = expo^(-lambda);
for it = 1:N
    k = 0;
    u = rand(1,1);
    p_single = p_initial;
    threshold = p_initial;
    while u > threshold
        amp = amp_c / (k+1);
        p_single = p_single * amp;
        threshold = threshold + p_single;
        k = k+1;
    end
    X(it) = k;
end
end
 ```
![My helpful screenshot](/img/Generation of random variables/Generators of random variables d5.png)
## 3.2. Acceptance-Rejection method
We first give an example how to generate a uniformly distribution on a complicated bounded set. Secondly, we give examples of how to use acceptance-rejection method to generate a normal distributed random variable with the aid of Laplace distribution or Cauchy distribution.
### Uniformly elliptic distribution
Although ellipse is not so complicated a graph but here is just for illustrating how to use the acceptance-rejection method in practice.
``` matlab
function [X] = ar_ellipce(N)
X = zeros(2,N);
XL = 0;
pick = @(x,y) 2 - x^2 / 8 - y^2;
while (XL < N)
    U = rand(2,1);
    U = [8 0 ; 0 sqrt(8)] * U - [4;sqrt(2)];
    if pick(U(1,1),U(2,1)) > 0
        XL = XL+1;
        X(:,XL) = U;
    end
end
```
![My helpful screenshot](/img/Generation of random variables/Generators of random variables 9.png)
### Normal distribution by Cauchy distribution
We use unormalized density of Cauchy distribution to be the dominated function to generate normal distributed random variable.
```matlab
function [X] = ar_gaussiancauchy(N)
pick = @(x,y) 1/(sqrt(2 *pi)) * exp( -x^2/2) - y;
f0 = @(x) sqrt(2*pi/exp(1)) / (pi * (1 + x^2));
X = zeros(1,N);
XL = 0;
while XL < N
    U = rand_cauchy(0,1,1);
    H = f0(U) * rand(1);
    if pick(U,H) >=0
        XL = XL+1;
        X(XL) = U;
    end
end
end
```
```matlab
gaussian = @(x,y) 1/(sqrt(2 *pi)) * exp( -x.^2./2) ;
unnormalized_cauchy = @(x) sqrt(2*pi/exp(1)) ./ (pi * (1 + x.^2));
N = 10^5;
[X] = ar_gaussiancauchy(N);
[number, center] = hist(X,10^2);
bar(center, number/N/(center(2)-center(1)));
hold on
plot(center,gaussian(center),'r')
plot(center,unnormalized_cauchy(center),'g')
legend('normalized histogram','normal distribution','unnormalized cauchy distribution')
hold off
```
![My helpful screenshot](/img/Generation of random variables/Generators of random variables 10.png)
### Normal distribution by Laplace distribution
We use unormalized density of Laplace distribution to be the dominated function to generate normal distributed random variable.
```matlab
function [X] = ar_gaussianlaplace(N)
pick = @(x,y) 1/(sqrt(2 *pi)) * exp( -x^2/2) - y;
f0 = @(x) sqrt(2*exp(1)/pi) * exp(-abs(x))/2;
X = zeros(1,N);
XL = 0;
while XL < N
    U = rand_laplace(1,1);
    H = f0(U) * rand(1);
    if pick(U,H) >=0
        XL = XL+1;
        X(XL) = U;
    end
end
end
```
```matlab
gaussian = @(x,y) 1/(sqrt(2 *pi)) * exp( -x.^2./2) ;
unnormalized_laplace = @(x) sqrt(2*exp(1)/pi) * exp(-abs(x))/2;
N = 10^5;
[X] = ar_gaussianlaplace(N);
[number, center] = hist(X,10^2);
bar(center, number/N/(center(2)-center(1)));
hold on
plot(center,gaussian(center),'r')
plot(center,unnormalized_laplace(center),'g')
legend('normalized histogram','normal distribution','unnormalized laplace distribution')
hold off
```
![My helpful screenshot](/img/Generation of random variables/Generators of random variables 11.png)
## 3.3. Methods for Normal distribution
First we present the Box-Muller method and the Masaglia method. Notice that these are methods for even dimensional normal distribution so even though you only need 3, you have to compute for 4. Next we give the algorithm of general normal distribution with the normal number generator in matlab with an example.
### Box Muller method
```matlab
function [X] = boxmuller(N0)
N = 2 * ceil(N0/2);
X =zeros(N,1);
XL = 0;
while XL < N
    R = sqrt(rand_exp(0.5,1));
    ARG = rand(1) * 2 * pi;
    X1 = R * sin(ARG);
    X2 = R * cos(ARG);
    X(XL+1) = X1;
    X(XL+2) = X2;
    XL = XL+2;
end
X = X(1:N0);
end
```
### Marsaglia method
```matlab
function [X] = marsaglia(N0)
N =  2 * ceil(N0/2);
X = zeros(1,N);
XL = 0;
while XL < N
    X1 = rand(1)*2 - 1;
    X2 = rand(1)*2 - 1;
    r2 = X1^2 + X2^2;
    if (r2 < 1) && (r2 > 0)
        X(XL+1:XL+2)= [X1,X2] * sqrt(-2*log(r2)) / sqrt(r2);
        XL = XL+2;
    end
end
X = X(1:N0);
end
```
### General normal distribution
We use the default cholesky decomposition function in matlab to find the Weight of affine linear transformation. Also, for simplicity we use the normal number generator in matlab.
```matlab
function [X] = normal(Q,nu,N)
m = length(nu);
X = chol(Q)' *randn(m,N) + nu * ones(1,N);
end
```
### Application of stimulate the path of Brownian motion
Notice that the finite dimensional distribution of standard brownian motion is a multi-dimensional distribution. This allows us to use the general normal distributed random variable generator introduced above to stimulate the sample path of standard brownian motion on any finite time partition.
```matlab
function X = standardbownianmotion(t)
I = t > 0;
N = sum(I);
t = t(I);
P = ones(length(t),1)*t;
Q = min(P,P');
X = zeros(N,1);
X(I) = chol(Q)' * randn(N,1);    
end
```
```matlab
N = 10^3;
preimage = 0:1/N:1;
X = standardbownianmotion(preimage);
plot(preimage,X);
hold on
X = standardbownianmotion(preimage);
plot(preimage,X);
hold on
X = standardbownianmotion(preimage);
plot(preimage,X);
```
![My helpful screenshot](/img/Generation of random variables/Generators of random variables 14.png)
## Reference

- [Lecture notes of Numerical Analysis of Stochastic Differential Equations by Prof. Dr. Arnulf Jentzen]( )
- [Monte Carlo Methods in Financial Engineering by Glasserman, Paul](https://www.springer.com/gp/book/9780387004518)
- [Random number generation Wikipedia](https://en.wikipedia.org/wiki/Random_number_generation)
- [Pseudo random number generator Wikipedia](https://en.wikipedia.org/wiki/Pseudorandom_number_generator)
- [Hardware random number generator Wikipedia](https://en.wikipedia.org/wiki/Hardware_random_number_generator)
- [Monte Carlo method Wikipedia](https://en.wikipedia.org/wiki/Monte_Carlo_method)
- [Multivariate normal distribution Wikipedia](https://en.wikipedia.org/wiki/Multivariate_normal_distribution)



