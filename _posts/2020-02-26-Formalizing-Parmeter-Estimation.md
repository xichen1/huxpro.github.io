---

layout:     post
title:    "Formalizing Parameter Estimation"
subtitle:   "CMPUT 296"
date:     2020-02-23
author:     "rick"
header-img: "img/post-c-language.png"
tags:
- Study note
---

We want to find some function or model which satisfied some requirements. First, the model should be able to have performance on the previously unseen data should not deteriorate(change) once the new data is presented. Second, function must be able to include information about the model space from which it is selected and process of selecting a model should be able to accept training "advice" from an analyst. Finally, when large amounts of data are available learning algorithms must be able to provide solutions in reasonable time given the resource.

In this section, we can use MAP and MLE to estimate some distribution's parameters (mean μ and SD σ for normal distribution λ for Poisson distribution.) 

#### MAP and Maximum likelihood Estimation(MLE)

Imagine there is a dataset of observations D={x<sub>i</sub>} (i from 1 to n). It has an unknown but true distribution p*. However, if you know the distribution is in a set of possible distribution, F, F is called the hypothesis space or function class. For example, F can be the family of all univariate Gaussian distributions. In this family, the mean μ\* and SD σ\* can be different. F = {N(μ, σ^2) | for any μ ∈ R and σ ∈ R+}. While the true distribution has parameters μ\*, σ\*, we need to find μ and σ as close to the true ones as possible.

The idea of MAP estimation is to find the most probable model for the observed data. Given the dataset D, the solution of MAP is f<sub>MAP</sub> = argmax<sub> f∈F</sub> p(f|D).

p(f|D) is called the posterior distribution of the model given the data. MAP estimate is exactly the most probable model. 

To calculate the posterior distribution we apply he Bayes rules: 

p(f|D) = p(D|f)p(f)/p(D)

p(D|f) is called the likelihood function, p(f) is the prior distribution of the model. p(D) is the marginal distribution of the data.

To compute p(D), we need to sum all situations with different f ∈ F. p(D) = sum(p(D|f)*p(f)).

max <sub>fF</sub> p(D|f)p(f)/p(D) = 1/p(D) * max <sub>f∈F</sub> p(D|f)p(f). P(D) is not related with the MAP solution. Now f<sub>MAP</sub> = argmax<sub> f∈F</sub> p(D|f)p(f). If in some situations, we cannot prefer one model and have the same p(f) for all f in the hypothesis space. Then MAP becomes MLE. f<sub>MLE</sub> = argmax <sub>f∈F</sub> p(D|f).  (The p(f) is not considered). So MLE can be seen as a special case of MAP.

EX: Suppose data set D = {2,5,9,5,4,8} is an i.i.d. sample from a Poisson distribution with a fixed but unknown parameter λ<sub>0</sub>. Find the MLE solution of λ<sub>0</sub>.

λ<sub>MLE</sub> = argmax p(D|λ)

p(D|λ) = p({x<sub>i</sub>}|λ) = p(x<sub>1</sub>|λ)p(x<sub>2</sub>|λ)\*...\*p(x<sub>i</sub>|λ)

To find a λ to make the p maximum. ln(p(D|λ)) = ln(p(x<sub>1</sub>|λ)p(x<sub>2</sub>|λ)\*...\*p(x<sub>i</sub>|λ))

= sum(ln(p(x<sub>i</sub>|λ)))

In Poisson distribution p(x|λ)=λ^x*e^(-λ)/x!, ln(p(x|λ)) = ln(λ^x)+ln(e^(-λ))-ln(x!) = x*ln(λ)-λ-ln(x!)

sum(ln(p(x<sub>i</sub>|λ))) = sum(x<sub>i</sub>ln(λ)) - nλ - sum(ln(x!))

By computing the first derivative, we can compute the λ which makes ln.. max.

d ln(p(D|λ))/d λ = (1/λ)sum(x<sub>i</sub>) - n. In this case, n = 6. λ=sum(x<sub>i</sub>)/n



Ex of MAP: D = {2,5,9,5,4,8}. i.i.d. sample from Poisson with mean λ<sub>0</sub>. We need to calculate the MAP estimate of λ<sub>0</sub>. Some other information is given. Suppose the prior knowledge about λ<sub>0</sub> can be expressed using a gamma distribution with k=3 and θ=1. Find the MAP of λ<sub>0</sub>. 

By gamma distribution, p(λ) = λ^(k-1)e^(-λ/θ)/θgamma

By Poisson distribution, p(x|λ) = λ^x*e^-λ/x!

 λ<sub>MAP</sub> = argmax <sub>λ∈(0, ∞)</sub> p(D|λ)p(λ). Taking log to simplify.

ln p(D|λ)p(λ) = ln(p(D|λ)) + ln(p(λ)) = ln sum(p(x<sub>i</sub>|λ)) + ln p(λ)

ln p(λ) = ln λ^(k-1)e^(-λ/e)/θgamma(k) = ln  λ^(k-1) + ln e^(-λ/e) - ln θgamma(k) = (k-1) ln λ - (λ/θ) - ln θgamma(k)

sum(ln (λ^x<sub>i</sub>*e^-λ/x<sub>i</sub>)) = sum(x<sub>i</sub>*ln λ - λ - ln x<sub>i</sub>) = ln λ sum(x<sub>i</sub>) - nλ - ln sum(x<sub>i</sub>)

Taking derivate: d(ln p(D|λ)p(λ)) / d λ= sum(x<sub>i</sub>)/λ - n + (k-1)/λ - 1/θ = 0

sum(x<sub>i</sub>) + (k-1) = (n + 1/θ)λ

So λ<sub>MAP</sub> = (k-1 + sum(x<sub>i</sub>))/(n + 1/θ) = (3-1+(2+5+9+5+4+8))/(6+1) = 35/7 = 5



##### The effect of the amount of data

When the data amount is large, the result of MAP becomes closer to MLE. The importance of prior is reduced.

An example of Poisson distribution: s<sub>n</sub> = sum(x<sub>i</sub>), which is from the random variable S<sub>n</sub> = sum(X<sub>i</sub>) . And suppose s<sub>n</sub>/n^2 --> ∞ when n --> ∞.

![MLE-MAP](C:\Users\ppx\Desktop\web1111\xichen1.github.io\img\MLE-MAP.JPG)

Ex: Let D={x<sub>i</sub>}, i from 1 to n. It is an i.i.d. sample from a normal distribution. To find the MLE of the parameters.

By taking partial derivatives of μ, σ, we get the result μ<sub>MLE</sub> = 1/n(sum(x<sub>i</sub>)), σ<sub>MLE</sub> = 1/n(sum(x<sub>i</sub>-μ<sub>MLE</sub>)^2).





#### Bayesian estimation

Maximum a posterior and maximum likelihood approaches report the solution that is consistent with the mode of the posterior distribution and the likelihood function. But the MLE and MAP cannot deal with the skewed distributions and multimodal distributions. Bayesian can!

