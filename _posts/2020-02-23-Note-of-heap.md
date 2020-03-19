---

layout:     post
title:    "Note heap"
subtitle:   "CMPUT 204"
date:     2020-02-23
author:     "rick"
header-img: "img/post-c-language.png"
tags:
- Study note
---

Some alg and time complexity of heap:

##### Max-heapify =  Θ(logn) =  Θ(h)

```
Max-Heapify(A,i)
		**pre-conditition: tree rooted at A[i] is and almost-heap
	lc <-- leftchild(i)
	rc <-- rightchild(i)
	largest <-- i
	if (lc <= heapsize(A) and A[lc] > A[largest]) then
		largest <-- lc
	if (rc <= heapsize(A) and A[rc] > A[largest]) then
		largest <-- rc
	if (largest != i) then
		exchange A[i] <--> A[largest]
		Max-heapify(A,largest)
```

The WC is from the top of the heap to the bottom of the heap. Every time it costs Θ(1) and in total it is h*Θ(1) = Θ(h) = Θ(logn).

##### Build-Max-Heap =  Θ(n) 

```
Build-Max-Heap(A)
		** turn an array into a heap
	heapsize(A) <-- length[A]
	for (i <-- floor(length[A]/2) downto 1) do
		Max-heapify(A,i)
```

##### Heap sort =  Θ(nlogn)

```
Heap-Sort(A,n)
		** sort an array using a heap
	Build-Max-Heap(A)
	heapsize <-- n
	while (heapsize > 1) do
		exchange A[1] <--> A[heapsize]
		heapsize <-- heapsize - 1
		Max-Heapify(A[1...heapsize],1)
```

 For each position i = n, n-1, n-2, ... , 2, Max-Heapify takes O(logn). Totally, it costs Θ(nlogn).

![](C:\Users\ppx\Desktop\Capture.JPG)

#### Priority Queue

##### Initialize(A) = Θ(n)

Building a heap

##### Extract-Maximum(A) = Θ(logn)

```
Heap-Extract-Max(A)
		precondiction: A is not empty
	max <-- A[1]
	A[1] <-- A[heapsize[A]]
	heapsize[A] <-- heapsize[A] - 1
	if (heapsize[A]>0) then
		Max-Heapify(A,1)
	return max
```

The exchange costs Θ(1) and max heapify costs Θ(logn).

##### Heap-Increase-Key (A, i, key) = Θ(logn)

```
Heap-increase-Key(A, i, key)
		** precondiction: key >= A[i]
	A[i] <-- key
	while (i>1 and A[parent(i)]>A[i]) do
		exchange A[i] <--> A[parent(i)]
		i <-- Parent(i)
```

From the bottom to the top of the heap, it takes Θ(h) = Θ(logn)

##### Insert-Key (A, new_key) = Θ(logn)

```
Insert-Key(A,new_key)
	heapsize[A] <-- heapsize[A]+1
	A[heapsize[A]] <-- $$-/infty$$
	Heap-Increase-key(A, heapsize[A], key)
```

