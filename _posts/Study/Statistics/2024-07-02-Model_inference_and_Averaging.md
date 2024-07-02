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

$\hat{\theta}_{MLE} = \arg\max{\theta}L(\theta; x) = \arg \max_{\theta}P(x \mid \theta)$

**Score** function $j(\theta; Z) = \sum_{j=1}^N j(\theta; z_j)$ , where $j(\theta; Z) = \frac{\partial l (\theta; z_i)}{\partial \theta}$

**Information** matrix $I(\theta) = -\sum_{i=1}^N \frac{\partial^2{l(\theta;z_i)}}{\partial \theta \partial \theta^{T}}$

**Fisher** information $i(\theta) = E_{\theta}[I(\theta)]$

### Sampling distribution of $\hat{\theta}$
$N(\hat{\theta}, i(\hat{\theta})^{-1})$ or $N(\hat{\theta}, I(\hat{\theta})^{-1})$

### Estimation for the standard errors of $\hat{\theta}_j$
$\sqrt{i(\hat{\theta})^{-1}_{jj}}$ and $\sqrt{I(\hat{\theta})^{-1}_{jj}}$

### Confidence points for $\theta_j$
$\hat{\theta}_j\pm z(1-\alpha)\cdot\sqrt{\left[i(\hat{\theta})^{-1}\right]_{jj}}$ or $\hat{\theta}_j\pm z(1-\alpha)\cdot\sqrt{\left[I(\hat{\theta})^{-1}\right]_{jj}}$

### More accurate CI of $\theta_j$
$2\left[l(\hat{\theta}) - l(\theta_0)\right]\sim \chi^{2}_p$


# Bayesian methods

A sampling model $Pr(Z \mid \theta)$

A prior distribution for the parameters $Pr(\theta)$

Posterior distriubution $Pr(\theta \mid Z) = \frac{Pr(Z \mid \theta)\cdot Pr(\theta)}{\int_{}^{} Pr(Z \mid \theta)\cdot Pr(\theta) d\theta}$

The posterior distributoin provides the basis for predicting the values of a future observation $z^{new}$ via the predictin distribution

$Pr(z^{new} \mid Z) = \int_{}^{} Pr(z^{new} \mid \theta)\cdot Pr(\theta \mid Z)d\theta$

# EM algorithm
![image](https://github.com/JeonSHyun/JeonSHyun.github.io/assets/86886562/2dfcbae4-0e8c-4b05-9abc-84c7973bdd59)


# Bagging (Bootstrap aggregating)
The emsemble learning method that is commonly used to reduce variance within a noisy dataset.

$L$ is training dataset and $L1, L2, ...$ is bootstrap samples.

$\phi(x \mid L1), \phi(x \mid L1), ...$ is learning models.

**Regression** $\phi_B(x) = \frac{1}{B}\sum_{b=1}^B\phi(x, L_b)$

**Classification** $\phi_B(x) = Mode \phi(x, L_b)$

## Hard voting and Soft voting


# Model Averagng and stacking

Stacking is an ensemble learning technique that combines multiple individual models to improve predictive performance.

## Bayesian model Averaging

$M_m(m = 1, ...M)$ is training set $Z$.

Suppose $\zeta$ is some quantity of interest, for example, a predition $f(x)$ at some fixed feature value $x$.
The posterior distribution of $\zeta$ is $Pr(\zeta \mid Z) = \sum_{m=1}^M Pr(\zeta \mid M_m, Z)Pr(M_m \mid Z)$

And posterior mean is $E(\zeta \mid Z) = \sum_{m=1}^M E(\zeta \mid M_m, Z)Pr(M_m \mid Z)$

## Frequentist model Averaging
$M_m(m = 1, ..., M)$ is candidate models for our training set Z.

$x$ is fixed and the N observatoins in the dataset Z are distributed according to P.

Given predictors $\hat{f_1(x)}, \hat{f_2(x)}, ..., \hat{f_M(x)}$, under squared-error loss, we can seek weights $\hat{w} = (w_1, w_2, ..., w_M)$ such that $\hat{x} = \arg \min_w E_P left[Y-\sum_{m=1}^M w_M \hat{f_m(x)^2}$

## Generalized Stacking
$\hat{w}^{st} = \arg \min_w \sum_{i=1}^N \left[ y_i - \sum_{m=1}^M w_m \hat{f_m^{-i}(x_i)} \right]$

By using the cross-validated predictors $\hat{f_m^{-i}(x_i)}$, stacking avoids givint unfairly high weight to models with higher complexity.
