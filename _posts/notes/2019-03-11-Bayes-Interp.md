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

## The Evidence and the Occam Factor

We can write Bayes rule for each of the two levels of inference discussed previously.

### First Level: Model Fitting

If we assume one of the models, $$H_i$$ is true, we infere the model parameters, $\vec{w}$, given the data, $D$. Bayes rule is then,

$$\begin{equation} P(\vec{w} | D, H_i)= \frac{P(D|\vec{w},H_i) P(\vec{w}|H_i)}{P(D|H_i)}\end{equation}$$
