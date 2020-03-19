---
layout:     post
title:    "Note of ML Optimization"
subtitle:   "unfinished note"
date:     2020-02-22
author:     "rick"
header-img: "img/post-c-language.png"
tags:
- Study note
---

#### The basic optimization problem and stationary points

The goal of optimization is to find and select a set of parameters $ w \in R<sup>d </sup>$ to minimize the objective function c: 



$$
min \ c(w)\ (w\in R^d)
$$



The way to select and find w which minimizes the objective. The most straightforward way is to generate random w and check c(w). If any new generated w<sub>t</sub> has better performance than the previous best w, c(w<sub>t</sub>) < c(w), then w<sub>t</sub>  to be the new optimal solution. 

For the smooth and continuous function, we can use gradient descent (梯度下降). The gradient (derivative) can tell us where the derivative is zero and this place is somewhere the c(w)'s trend changes.

By Taylor series approximation 
$$
c(w)=\sum_{n=0}^{\infty}{((c^n)(w_n)/n!)(w-w_0)^n}
$$
The first three terms' sum is: 

$$
c(w)\approx \hat{c}(w)=c(w_0)+(w-w_0)c'(w_0)+1/2(w-w_0)^2c''(w_0)
$$

To find the zero derivative of c(w), we need to let $ c'(w) = 0 $. So we only need the first two terms.

$$
c'(w)\approx c'(w_0)+(w-w_0)c''(w_0)=0
$$
Then,

$$
w=w_0-c'(w_0)/c''(w_0)
$$
In the end, the formula for the gradient descent is w<sub>t+1</sub> =w<sub>t</sub> - n<sub>t</sub> c'(w<sub>t</sub>).

n<sub>t</sub> is the rate of learning. In this formula, the new x-value = the old x-value  -  learning rate*old derivate.

The way to choose n<sub>t</sub>. We can conduct a line search. Set a range for the n, (0, n<sub>max</sub>], from the n<sub>max</sub>, we can reduce n if the step size is too large by changing the factor t which belongs to [0.5,0.9]. When t is 0.9, it reduces n very slowly and when t is 0.5, it reduces n very quickly.



#### Optimization properties

##### Maximizing vs. minimizing

argmin c(w) = argmax (-c(w))

It means that the value w which makes c(w) minimal is same as the value w which makes -c(w) maximum. However, note that min c(w) != max -c(w).

##### Convexity

A function is convex if we draw a line between any two points on the function and the value between the two points lie below the line. Convexity makes sure that every critical point is local minimum. And therefore, the solution we get from the right step size is always optimal. The concave function is all values between two points are above the line.

##### Uniqueness of the solution

For some questions, we need to find the unique solution but sometimes we do not need to.

##### Equivalence under a constant shift

Adding or multiplying by a constant a != 0 does not change the solution:
$$
argmin \ c(w)=argmin (\ a\ c(w)) = argmin (\ a\ c(w)+a )
$$
