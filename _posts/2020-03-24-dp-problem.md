---

layout:     post
title:    "Some dp problems"
subtitle:   "dynamic programming"
date:     2020-03-24
author:     "rick"
header-img: "img/post-c-language.png"
tags:
- Problem
---

#### Matrix chain multiplication (矩阵链乘积)

Suppose we can several input matrices $$ A_1 $$ with dimensions $$d_0*d_1$$, $$ A_2 $$ with dimensions $$ d_1*d_2 $$, ..., $$ A_n $$  with dimensions $$ d_{n-1}* d_n $$. And we want to get the output$$ A_1* A_2*... * A_n$$ and using the minimum number of scalar multiplication (the multiplication between numbers). Suppose we want to multiply $$A_1 and A_2$$, we will have $$d_0*d_1*d_2$$ scale multiplications. 

Note: When $$A_1$$ with dimensions $$d_0, d_1$$ times$$A_2$$ with dimensions $$d_1, d_2$$, the result is the matrix with dimensions $$d_0, d_2$$.

So here is an example of different combinations of matrix multiplication: n=4, (d0,d1,d2,d3,d4) = (5,2,6,4,3)

$$((A1 *A2) *A3) * A4 \ is\ d0 *d1 *d2 + d0 * d2 *d3 + d0 *d3 * d4 = 5 * 2 * 6 + 5 * 6 * 4 + 5 * 4 * 3 = 240$$

$$ (A1 × (A2 × A3)) × A4 \ is \ d_1 * d_2 * d_3 + d_0 * d_1 * d_3 + d_0 * d_3 * d_4 = 148$$

and so on.

##### Recursion solution

Consider (A_1 * ... * A_i) * (A_i+1 * ... * A_n), the multiplication number is d_0 * d_i * d_n. In the next recursion, we need to find the least-costly way to multiply first i and the last n-i matrixes. For i, there are n-1 positions to stay, i.e. 1,2, ..., n-1. 

So we get the equation $$R(1, n) = min_{1\leq i \leq n-1} (d_0 * d_i * d_n + R(1,i) + R(i+1, n)) $$. The base case is R(i, i) for any i.

The runtime is $$\Omega ({3^n})$$

##### DP solution

Define M[i, j] (1 <= i <= j) is the minimal number of scalar multiplications needed to compute A_i * A_i+1 * ... * A_j.

Then 
$$
 \begin{cases}
	0, 			\ if\  i=j\\
	min_{i\leq k <j}(M[i,k]+M[k+1, j]+ d_{i-1}d_kd_j), \ if\ i<j
	\end{cases}
$$
