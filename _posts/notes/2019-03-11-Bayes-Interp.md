---
layout: post
title:  "Notes on Bayesian Interpolation"
categories: update
date:   2019-03-11 12:00:00 -1000
---

Random notes on the paper, [_Bayesian Interpolation_](http://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.27.9072) by David J.C. MacKay.

## Introduction

There are two levels of inference in data modelling:

**First level:** We assume one of the models created is true, and is to be fit to the data. Fitting this model typically involves inferring some set of optimal parameters &mdash;and their associated errors&mdash;given the data.

**Second level:** We compare available models and assign a ranking to the alternatives.

Model comparison is difficult because we can't just pick the model which fits the data best. The reason is, a high complex, and overly parameterized model will **always** fit data better. _Occam's razor_ is the principle that unnecessarily complex models should not be preferred over simpler ones. However, we will discover that Bayesian methods "automatically and quantitatively embody Occam's razor," where overly complex models are penalized.

___
## The Evidence and the Occam Factor

We can write Bayes rule for each of the two levels of inference discussed previously.

**First Level: Model Fitting**

If we assume one of the models, $$H_i$$ is true, we infere the model parameters, $$\mathbf{w}$$, given the data, $$D$$. Bayes rule is then,

$$P(\mathbf{w} \mid D, H_i)= \frac{P(D \mid \mathbf{w},H_i) P(\mathbf{w} \mid H_i)}{P(D|H_i)}$$

Often, the evidence for $$H_i$$ (denominator) is ignored because it is irrelevant to the first level of inference. Finding the maximum of the posterior is generally computed using gradient methods to find the most probable parameters, $$\mathbf{w}_{MP}$$. Error bars on these best fit parameters are obtained from the curvature of the posterior. If we define the Hessian,

$$\mathbf{A} = -\nabla\nabla \log P(\mathbf{w}|D,H_i)$$

and Taylor-expanding the $$\log$$ posterior with $$\Delta\mathbf{w}=\mathbf{w}-\mathbf{w}_{MP}$$,

$$P(\mathbf{w} \mid D,H_i) \simeq P(\mathbf{w}_{MP} \mid D, H_i)\exp \left(-\frac{1}{2} \Delta \mathbf{w}^T \mathbf{A} \Delta \mathbf{w}\right)$$

From this, we can see that the posterior can be locally approximated as a Gaussian with covariance matrix, $$\mathbf{A}^{-1}$$.

**Second Level: Model Comparison** At the second level, the posterior probability of each model,

$$P(H_i \mid D) \propto P(D \mid H_i)P(H_i)$$

The data dependent term, $$P(D \mid H_i)$$, is the evidence for $$H_i$$, which appears in the normalization constant in the first level posterior. "Inference is open ended: we continually seek more probable models to account for the data we gather. New models are compared with previous models by evaluating the evidence for them."

### A Modern Bayesian Approach to Priors
Classical Bayesian analysis deals with assigning the "right" priors for the problem. However, we can try many different priors and compare these alternative hypotheses by evaluating the evidence. Even if we try one hypothesis, and obtain an inaccurate prediction, we have still learned something. "A failure of Bayesian prediction is an opportunity to learn, and we are able to come back to the same data set with new hypotheses using new priors for example."

### Evaluating the Evidence

The evidence,

$$P(D \mid H_i) = \int P(D \mid \mathbf{w}, H_i)P(\mathbf{w} \mid H_i)d\mathbf{w}$$

Generally, the posterior will display a strong peak at the most probable parameter $$\mathbf{w}_{MP}$$. Then the evidence can be approximated by the height of the peak of the integrand $$P(D \mid \mathbf{w}, H_i)P(\mathbf{w} \mid H_i)$$ times its width, $$\Delta \mathbf{w}$$:

$$\begin{align} P(D \mid H_i) &\simeq P(D \mid \mathbf{w}_{MP}, H_i)P(\mathbf{w}_{MP} \mid H_i) \Delta\mathbf{w} \\ \text{Evidence} &\simeq \text{ (Best fit likelihood) } \text{ (Occam factor) } \end{align}$$
