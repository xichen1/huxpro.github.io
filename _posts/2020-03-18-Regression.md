---

layout:     post
title:    "Linear Regression and polynomial regression"
subtitle:   "CMPUT 296"
date:     2020-03-18
author:     "rick"
header-img: "img/post-c-language.png"
tags:
- Study note
---

To learn the relationship between features and targets (x_i and y_i), we usually hypothesize the functional form of the relationship. The function can be linear or non-linear. e.g. f(X) = w0+w1x1+w2x2 and f(X) = a + bX1X2. The w0 w1 w2 and a and b are the parameters need to be learned.

In particular, the linear function is modeled as a linear combination of features (x) and parameters (w), i.e. f(X) = w0 + w1x1 + ... + wdxd = sum(wjxj) = x^T w. We can extend x as (x0=1, x1, x2 ...  xd). This form allows us use the dot product. Finding the best parameters (w0 to wd) isreferred to as the linear regression problem.

#### Formalizing the maximum likelihood problem

Assume the observed data set D is a product of a data generating process in which n data points were drawn independently and according to the same distribution p(x). Assume the target variable Y has the linear relationship with input variable X, existing some error term  Ɛ. And the Ɛ follows the Gaussian distribution where the mean is zero. Y = sum(wjXj) + Ɛ. X0=1 is the intercept term. The assumption of normality for the error term is reasonable because of the central limit theorem.
$$
p(y|x,w) = (1/\sqrt(2\pi\sigma^2))exp(-(y-x^Tw)^2/2\sigma^2)
$$
