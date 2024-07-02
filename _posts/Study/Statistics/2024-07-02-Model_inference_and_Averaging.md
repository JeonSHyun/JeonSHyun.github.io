---
title: Model inference and Averaging
author: JSH
date: 2024-07-02 10:08:00 +0800
categories: [Study, Statistics]
tags: [Study, Statistics]
use_math: true
---

# Model inference
Inference is a process of using a trained model to infere a result from live data.


# Bootstrap and Maximum Likelihood

## Parametric bootstrap is closer to MLE than LSE

### Parametric bootstrap
Generating new datasets by using the estimated parameters of a model.
If a model assumes the data follows a normal distribution with a certain mean and variance, the parametric bootstrap uses theses parameters to create new simulated datasets.
In general, the parametric bootstrap agrees not with least squares but with maximum likelihood.

### Maximum Likelihood Estimation
Finding the parameter values that maximize the likelihood of observing the given data.

### Least Squres Estimation
Finding the parameter values that minimize the sum of the squared differences between the observed values and the values predicted by the model.

## Maximum likeelihood inference

### Probability density function
$z_{i}\sim g_{\theta}(z)$ e.g., if $Z\sim N(\mu, \sigma^{2}), \theta\sim (\mu, \sigma^{2})$

$g_{\theta} = \frac{1}{\sqrt{2\pi}\sigma}a^{-\frac{1}{2}(z-\mu)^{2}/\sigma^{2}}$

### Maximum Likelihood inference

**Likelihood** function $L(\theta; Z) = \prod_{i=1}^N g_\theta (z_i)$

**Loglikelihood** function $l(\theta; Z) = \prod_{i=1}^N \log{g_\theta (z_i)}$

$\hat{\theta}_{MLE} = \arg\max_{\theta} L(\theta; x) = \arg \max_{\theta} P(x|\theta)$

**Score** function $j(\theta; Z) = \sum_{j=1}^N j(\theta; z_j)$ , where $j(\theta; Z) = \frac{\partial l (\theta; z_i)}{\partial \theta}$

**Information** matrix $I(\theta) = -\sum_{i=1}^N \frac{\partial^2{l(\theta;z_i)}}{\partial \theta \partial \theta^{T}}$

**Fisher** information $i(\theta) = E_{\theta}[I(\theta)]$


# Bayesian methods


# EM algorithm


# Bagging


# Model Averagng and stacking

