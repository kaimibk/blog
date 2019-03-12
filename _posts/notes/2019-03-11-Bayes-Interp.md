---
layout: post
title:  "Notes on Bayesian Interpolation"
categories: update
date:   2019-03-11 12:00:00 -1000
---

My notes on the paper, [_Bayesian Interpolation_](http://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.27.9072) by David J.C. MacKay.

## Introduction

There are two levels of inference in data modelling:

**First level:** We assume one of the models created is true, and is to be fit to the data. Fitting this model typically involves inferring some set of optimal parameters &mdash;and their associated errors&mdash;given the data.

**Second level:** We compare available models and assign a ranking to the alternatives.

Model comparison is difficult because we can't just pick the model which fits the data best. The reason is, a high complex, and overly parameterized model will **always** fit data better. _Occam's razor_ is the principle that unnecessarily complex models should not be preferred over simpler ones. However, we will discover that Bayesian methods "automatically and quantitatively embody Occam's razor," where overly complex models are penalized.

___
## The Evidence and the Occam Factor

We can write Bayes rule for each of the two levels of inference discussed previously.

### First Level: Model Fitting

If we assume one of the models, $$H_i$$ is true, we infere the model parameters, $$\mathbf{w}$$, given the data, $$D$$. Bayes rule is then,

$$\begin{equation} P(\mathbf{w} \middle D, H_i)= \frac{P(D \middle \mathbf{w},H_i) P(\mathbf{w} \middle H_i)}{P(D|H_i)}\end{equation}$$

Often, the evidence for $$H_i$$ (denominator) is ignored because it is irrelevant to the first level of inference. Finding the maximum of the posterior is generally computed using gradient methods to find the most probable parameters, $$\mathbf{w}_{MP}$$. Error bars on these best fit parameters are obtained from the curvature of the posterior. If we define the Hessian,

$$\mathbf{A} = -\nabla\nabla \log P(\mathbf{w}|D,H_i)$$

and Taylor-expanding the $$\log$$ posterior with $$\Delta\mathbf{w}=\mathbf{w}-\mathbf{w}_{MP}$$,

$$\begin{equation}P(\mathbf{w} \middle D,H_i) \simeq P(\mathbf{w}_{MP} \middle D, H_i)\exp (-\frac{1}{2}\Delta \mathbf{w}^T \mathbf{A} \Delta \mathbf{w})\end{equation}$$
