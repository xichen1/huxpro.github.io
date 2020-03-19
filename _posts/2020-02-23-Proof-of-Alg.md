---

layout:     post
title:    "Proof of Alg."
subtitle:   "CMPUT 204"
date:     2020-02-23
author:     "rick"
header-img: "img/post-c-language.png"
tags:
- Study note
---

If the code is written using recursion, prove correctness using induction.

##### Loop invariant

For code written using loops, prove correctness by the loop invariant method.

A loop-invariant is an assertion about the state of the code that is always true at the beginning of each loop-iteration. Two steps of using loop-invariant: 1. identify the LI. 2. prove the LI for initialization, maintenance, termination#1 (stop eventually), termination#2 (right result).

One example:

```
FindSum(A,n)
	sum <-- A[1]
	j <-- 2
	while (j<=n)
		sum <-- sum + A[j]
		j <-- j+1
	return sum
```

The LI is "At the beginning of each loop iteration, sum = (j-1)sum(i=1)A[i]".

###### The proof of LI

Initially: Before the loop begins sum = A[1] = A[1,...,(2-1)]

Maintenance: Suppose that at the beginning of iteration j, sum=A[1]+A[2]+...+A[j-1]. Then at the beginning of iteration j+1. Sum<sub>after</sub>=sum<sub>before</sub>+A[j] = A[1]+A[2]+..+A[j] = A[1]+A[2]+..+A[j+1-1].

Termination #1: The loop terminates as we only increase j, so eventually j>n.

Termination #2: When the while-loop terminates, j=n+1, in that case LI implies sum = A[1]+...+A[n].