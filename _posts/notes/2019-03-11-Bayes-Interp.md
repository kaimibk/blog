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

The evidence term is found by multiplying the likelihood by the Occam factor. This is a term with magnitude less than one that penalizes $$H_i$$ for having the parameter $$\mathbf{w}$$.

### Interpretation of the Occam Factor

The posterior uncertainty in $$\mathbf{w}$$ is $$\Delta \mathbf{w}$$. If we adopt an uninformative prior for $$P(\mathbf{w} \mid H_i)$$ on the interval $$\Delta^0\mathbf{w}$$---which represents the range of possible parameters before the data arrives. Thus,

$$P(\mathbf{w}_{MP} \mid H_i) = \frac{1}{\Delta^0 \mathbf{w}}$$

$$\Rightarrow \text{ Occam Factor } = \frac{\Delta\mathbf{w}}{\Delta^0\mathbf{w}}$$

That is to say, it is the ratio of the posterior accessible volume of $$H_i$$'s parameter space to the prior accessible volume. It can also be thought of as the factor by which $$H_i$$'s parameter space collapses when the data arrives. Additionally, the $$\log$$ of the Occam factor can be interpreted as the amount of information we gain about the model $$H$$ when the data arrives.

In summary, a complex model which is highly parameterized will be penalized with a larger Occam factor than a simpler one. The model which achieves the greatest evidence is determined by a trade-off between minimizing this natural complexity measure and minimizing the data misfit.

**Comments:**
- To evaluate the Occam factor all we need is the Hessian $$\mathbf{A}$$. That is to say, Bayesian model comparison by evaluating the evidence is no more demanding than finding the optimal parameters and their associated errors.
- The log evidence, $$\log_2 P(D \mid H_i)$$, is the number of bits in the ideal shortest message that encodes the data, $$D$$ using the model $$H_i$$.

## The Noisy Interpolation Problem

Assume the data set to be interpolated is a set of pairs $$D={x_m, t_m}$$, where $$n\in{1...N}$$. To define an interpolation model, a set of fixed basis function $$A={\phi_h(x)}$$ is defined, and the interpolated function is assumed to have the form:

$$y(x) = \sum_{h=1}^{k} w_h\phi_h(x)$$

The data is modelled as deviating from this mapping under some additive noise process, $$t_m = y(x_m)+\nu_m$$. If $$\nu$$ is modelled as zero-mean gaussian with standard deviation $$\sigma_\nu$$, the likeihood is then,

$$P(D \mid \mathbf{w},\beta, A) = \frac{\exp(-\beta E_D(D \mid \mathbf{w}, A))}{Z_D(\beta)}$$

where $$\beta = 1/\sigma_\nu^2$$, $$E_D = \sum_m (y(x_m)-t_m)^2$$, and $$Z_D = (2\pi/\beta)^{N/2}$$. Finding the maximum likelihood parameters $$\mathbf{w}_{ML}$$ is an 'ill-posed' problem. The parameter $$\mathbf{w}$$ that minimizes $$E_D$$ is underdetermined or depends on the sensitively on the details of the noise in the data&mdash;the interpolant in those cases oscillates widely and starts to fit the noise.
