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

Assume the observed data set D is a product of a data generating process in which n data points were drawn independently and according to the same distribution p(x). Assume the target variable Y has the linear relationship with input variable X, existing some error term  Ɛ. And the Ɛ follows the Gaussian distribution where the mean is zero. $$ Y =  \sum_{j=0}^{d} w_j X_j + Ɛ $$ . X0=1 is the intercept term. The assumption of normality for the error term is reasonable because of the central limit theorem.
$$
p(y|x,w) = (1/\sqrt(2\pi\sigma^2))exp(-(y-x^Tw)^2/2\sigma^2)
$$

To implement the MLE problem,
$$
W_{MLE}=argmin_{w\in F} - \sum_{i=1}^n ln(p(y_i|x_i,w))
= argmin_{w\in F} \sum_{i=1}^n ln\sqrt{2\pi\sigma^2}+\sum_{i=1}^n (y_i-x_i^Tw)^2/2\sigma^2
$$
Only the second part is related with w, so
$$
= argmin_{w\in F} \frac{1} {2\sigma^2}*\sum_{i=1}^n (y_i-x_i^Tw)^2 \ = argmin_{w\in F}\sum_{i=1}^n (y_i-x_i^Tw)^2
$$
To find the w, we need to minimize the difference between real y_i and $$ \hat{y_i} $$ which is $$x_i^T w$$. So this follows the intuition.



E.g. Consider data set {(1,1.2), (2, 2.3), (3, 2.3), (4, 3.3)}. We want to find the max likelihood coefficients for f(x) = w_0 + w_1x. Note that there is one column in X which is ones because that can make w_0 times 1.

$$X= \begin{bmatrix} 1 & 1 \\ 1 & 2 \\ 1&3 \\ 1&4\\ \end{bmatrix}     w = \begin{bmatrix} w_0  \\ w_1 \\ \end{bmatrix}   y =  \begin{bmatrix} 1.2  \\ 2.3 \\ 2.3 \\ 3.3 \\ \end{bmatrix} $$

In the next section, we can use some new equation to get the answer of w.



#### Linear Regression solution

We define the squared errors $$c_i(W) = (f(x_i) - y_i)^2 = \frac{1} {2} (x_i^Tw - y_i)^2 $$. And $$c(w) = \frac {1} {n} \sum{i=1}^n c_i(w)$$. In this case, we can get the average squared error instead of a cumulative error. And this is same in the MLE problem because 1/n does not affect the w's effect in the equation.

 To solve the MLE problem, we usually get the gradient of the equation, $$ \nabla c(w) = \frac {1} {n} \sum_{i=1}^n \nabla c_i(w) $$

![](C:\Users\ppx\Desktop\ppx\xichen1.github.io\img\LR-solution.JPG)

This is the result for c_i and w_j. So for the c(w), we need to obtain the system of equations with d+1 variables and d+1 equations.
$$
\frac{1}{n} \sum_{i=1}^n(\vec{x_i^T}w - y_i)x_{i0}=0\\
\frac{1}{n} \sum_{i=1}^n(\vec{x_i^T}w - y_i)x_{i1}=0\\...\\
\frac{1}{n} \sum_{i=1}^n(\vec{x_i^T}w - y_i)x_{id}=0
$$
Which is same as 
$$
\frac{1}{n} \sum_{i=1}^n (\vec{x_i^T}w - y_i)\vec{x_i} = 0
$$


When we turn it as a linear algebra problem, we can define $$ \vec {A}=\frac{1}{n} \sum_{i=1}^n \vec{x_i} \vec{x_i^T}  \in R^{(d+1)*(d+1)}$$ 

$$ \vec {b}=\frac{1}{n} \sum_{i=1}^n \vec{x_i} \cdot y_i \in R^{d+1} $$

So $$ \vec {A} \cdot \vec {w} = \vec {b} $$. If A is invertible, then $$   \vec {w} =\vec {A^{-1}} \vec {b} $$.



##### Solve LR using gradient descent

In     gradient descent, we would initialize the weights $\vec {w}$ at some random initialization and iteratively update $\vec {w}$ until we reach a point where the gradient is near 0.

![](C:\Users\ppx\Desktop\ppx\xichen1.github.io\img\in-post\Rl\rl_gd.JPG)

Analysis of time cost:

Using gradient descent can be more quick than the linear algebra solution, each gradient descent update costs O(nd) and the solution to the linear system costs O(d^3 + d^2n). Constructing A costs O(d^2n) and inversing matrix using O(d^3). For gradient descent, the k iteration costs O(ndk).

To improve the efficient, we use stochastic gradient descent.

#### Stochastic gradient descent and handling Big Data sets

In stochastic approximation, we only use one sample or a small mini-batch of b samples (e.g., b = 32). For example, if we only use one sample, we can use this point to update the gradient:
$$
w_{t+1} <-- w_{t} - n_t(\vec{x_i^T}-y_i)\vec{x_i}
$$
