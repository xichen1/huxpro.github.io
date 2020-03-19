---
layout:     post
title:    "Note of ML Estimator"
subtitle:   "unfinished note"
date:     2020-02-22
author:     "rick"
header-img: "img/post-c-language.png"
tags:
- Study note
---



#### Estimate the expected value

For example, we have n random variables X<sub>1</sub>, X<sub>2</sub>, ... X<sub>n</sub>, where E[X<sub>i</sub>]= \mu and the mean \mu is unknown. The average estimator is 
$$
\bar{X}=(1/n)\sum_{i=1}^{n}{X_i}
$$
How can we check if the estimator is biased? The bias of the estimator is how far the expected value of the estimator from the true \mu. In formula,
$$
Bias(\bar{X})=E[\bar{X}]-\mu
$$
If the bias value if zero, the estimator is said to be unbiased. The E(\bar{x}) can reflect that the \bar{X} is random. Because if several experiments are conducted, there could be different E[\bar{X}].



We can compute the expectation of \bar{X}.
$$
\begin{split}
E[\bar{X}]&= E[(1/n)\sum_{i=1}^{n}{X_i}]\\
          &= (1/n)\sum_{i=1}^{n}{E[X_i]}\\
          &= 1/n\sum_{i=1}^{n}{\mu}\\
          &= (1/n)*n*\mu\\
          &= \mu
\end{split}
$$
It means that the expected value estimator is unbiased because the Bias is 0.

 