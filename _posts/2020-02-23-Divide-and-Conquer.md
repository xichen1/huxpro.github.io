---

layout:     post
title:    "Divide and Conquer"
subtitle:   "CMPUT 204"
date:     2020-02-23
author:     "rick"
header-img: "img/post-c-language.png"
tags:
- Study note
---

##### Merge-Sort

```
Merge(A, lo, mid, hi)
	**pre-condition: lo<=mid<=hi, A[lo,mid] and A[mid+1,hi] sorted
	**post-condition: A[lo,hi] sorted
	
Merge-sort(A,lo,hi)
	if lo<hi then
		mid = floor((lo+hi)/2)
		Merge-Sort(A,lo,mid)
		Merge-sort(A,mid+1,hi)
		Merge(A,lo,mid,hi)
```

Let denote #KC for a list of size n. Suppose the number of keys in the list is a power of 2.

T(n)=(n-1)+2*T(n/2).

To solve it: 1. Iterated substitution. 2. recurrence Tree 3. Guess and test. 4 Master Theorem

T(n) = 2T(n/2) + (n-1) = 2*(2*T(n/4)+(n/2-1))+(n-1)=4T(n/4)+(n-2)+(n-1) = 4(2T(n/8)+(n/4-1))+(n-2)+(n-1) = 8T(n/8)+(n-4)+(n-2)+(n-1) = 2^k*T(n/2^k)+(n-2^(k-1))+(n-2^(k-2))+...+(n-2^0)

The last one is T(1)=T(n/2^k) So let 2^k=n. T(n)=2^k*T(1) + (2^k-2^(k-1)) + (2^k-2^(k-2)) + ... + (2^k-2^0)= k*2^k-sum(2^i) (0<=i<=k-1) = k*2^k-(2^k-1)=(k-1)2^k+1.

2^k=n, k=logn. T(n) = (logn-1)n+1 =  O(nlogn)

To prove by induction: T(n) = (k-1)2^k+1    n = 2^k

Base case: T(1) = 0. k = 0, (0-1)2^0+1 = 1-1=0

Induction step. Suppose T(2^k) = (k-1)2^k+1, we need to prove that T(2^(k+1))=(k)2^(k+1)+1

T(2^(k+1))=(2^(k+1)-1)+2*T(2^k)= (2^(k+1)-1)+2*(k-1)2^k+2= 2^k+(2k-2)2^k+1=(k)*2^(k+1)+1







