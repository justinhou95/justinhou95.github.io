---
layout:     post
title:      Interesting questions
subtitle:   
date:       2021-01-15
author:     Songyan Hou 
header-img: img/questions/question.jpg
abstract: Some interesting questions from my friends
catalog: true
tags:
    - Interesting math
---

## Matmul in tensorflow and numpy

I found that matrix multiplication in tensorflow and numpy are different. 
{% highlight javascript %}
import numpy as np
import tensorflow as tf
a_tf = tf.random.normal([100,100],dtype = 'float64')
a = a_tf.numpy()
b_tf = tf.random.normal([100,100],dtype = 'float64')
b = b_tf.numpy()
c_tf = tf.linalg.matmul(a_tf,b_tf)
c = np.matmul(a,b)
print(c_tf.numpy() - c)
{% endhighlight %}
{% highlight Cscript %}
[[ 2.66453526e-15  1.77635684e-15 -8.88178420e-16 ... -1.77635684e-15
   1.77635684e-15  0.00000000e+00]
 [-3.10862447e-15  0.00000000e+00  1.77635684e-15 ...  2.44249065e-15
   8.88178420e-16  1.77635684e-15]
 [-5.32907052e-15  0.00000000e+00 -3.55271368e-15 ...  3.55271368e-15
   2.22044605e-15 -4.44089210e-16]
 ...
 [ 1.11022302e-16  1.33226763e-15 -1.77635684e-15 ...  3.55271368e-15
  -3.55271368e-15 -2.66453526e-15]
 [ 0.00000000e+00 -3.55271368e-15 -8.88178420e-16 ...  0.00000000e+00
  -2.22044605e-16 -1.66533454e-16]
 [-4.44089210e-16  1.77635684e-15 -3.55271368e-15 ... -3.55271368e-15
   0.00000000e+00  0.00000000e+00]]
{% endhighlight %}
My guess is that they use different procedure computing. Please email me if you know the reason behind. 

## Stationary? Or stationary increment?

I got a question from my friend: Why Brownian motion is stationary? I answered him without thinking: because independent increments only depend on time difference. However, immediately after I spoke out, I questioned myself: Wait, is Brownian motion really stationary? Of course not, how could $$B_0$$ equals to $$B_1$$ in distribution? What I had in mind is actually that Brownian motion has stationary increment. In our brain, it seems that Brownian motion is naturally linked with stationary but we should clarify to us that how they are linked in particularly.




