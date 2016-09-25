---
layout: post
title:  "Sampyl Package"
date:   2016-08-29 20:19:28 +0100
categories: jekyll update
---

Over the past few weeks I've really begun to appreciate the versatility of Python for data analysis as I have discovered a large number of powerful packages.

I'm going to look at a couple in the next two posts which I think are worth sharing.

Sampyl is a Python library, written by Mat Leonard, which implementing Markov Chain Monte Carlo (MCMC) samplers in Python. When used to its full potential it harnesses Bayesian parameter estimation and provides a collection of distribution log-likelihoods for use in constructing models. All of this without the need to learn unPuthonesque syntax/semantics.

Sampyl uses Autograd (see next post) when using Samplers such as NUTS which require gradients.

I love the ```jointplot``` using ```seaborn``` at the end of the example below (sampling from a 2D correlated normal distribution) which simultaneously shows individual distributions as well as correlation.


```python
%matplotlib inline

import sampyl as smp
from sampyl import np
import seaborn

icov = np.linalg.inv(np.array([[1., .8], [.8, 1.]]))
def logp(x, y):
   d = np.array([x, y])
   return -.5 * np.dot(np.dot(d, icov), d)

start = {'x': 1., 'y': 1.}
nuts = smp.NUTS(logp, start)
chain = nuts.sample(1000)

seaborn.jointplot(chain.x, chain.y, stat_func=None)
```

    Progress: [##############################] 1000 of 1000 samples


![png](/assets/sampyljsc.png)


