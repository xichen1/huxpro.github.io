---

layout:     post
title:    "Intro to Graph"
subtitle:   
date:     2020-04-11
author:     "rick"
header-img: 
tags:
- Study note
---

## Note from cmput 204

### Basic terminology

***V Nodes/ Vertices:*** A set of n elements with unique identifiers (1, 2, 3, ... , n).

***E Edges:*** 

For undirected graph: each edge is a set of exactly two nodes, e.g. e = {u, v}. u and v are nodes and we say e connects u and v. We also say u and v are adjacent or neighbors.

For directed graph: each edge is an ordered pair, e.g. e = <u, v>. We say u and v are adjacent. U is an in-neighbor of v and v is an out-neighbor of u. (u --> v).



***Adjacent*** can be the property between vertex and vertex or between edge and edge. e.g., 1 and 3 are adjacent. (1,2) and (2,5) are adjacent.

Incident can be the property between vertex and edge. e.g., 1 and (1,3) are incident.

***Loop/ self-loop:*** the edge is the form e = uu, which means the edge connect one node and the node itself.

***Degree of vertex:***  The number of edges that touch v. It is also known as the number neighbors of v.

***Path:*** A sequence of nodes v_0, v_1, ..., v_k such there exists k edges e_1, e_2, ..., e_k where e_i connect v_i-1 to v_i.

***Simple path:*** A path where all nodes are unique. Then since there are k edges, k is the length of the path.

***Cycle:*** A path where the start and the end vertex are the same, v_0 = v_k.

***A simple cycle:*** A cycle where all vertex except v_0 and v_k are unique. k is the length of the cycle.

***Size of the graph:*** \|G\| = number of vertex \|V\| = n

***Sub-graph:*** G' = (V', E') is a sub-graph of G = (V, E) if $$V' \subset V and E' \subset E$$. Removing an edge from G results in the subgraph (V, E \ {e})

***Induced subgraph:*** Let G = (V, E). And let $$ S \subset V $$ be any subset of vertices of G. Then the induced subgraph G[S] is the graph whose vertices set is S and the edge set contains all edges which connect nodes in S in G. Removing a node from G results in induced graph.

***Connectivity in an undirected graph:*** u is connected to v (u ~ v) if there exists a path from u to v. Note: otherwise, we can only say edge e connects the nodes u and v.

G is a connected graph if for every $$u,v \in V, u~v$$.

##### To be finished: 

Connected component, Forests and trees.

### Basic properties

A graph with n nodes and m edges. ***The range of m:***

For directed graph: The max number of edges is (n)*(n-1). The max situation is when every node connects to all the other nodes. There are n such situations so the total number is n*(n-1).

For undirected graph, e = (u,v) and x = (v,u) are the same edge and be counted as one edge. So the total number is n*(n-1)/2.

***The number of degree:*** 

For an undirected graph: $$ \sum_{v\in V} deg(v) = 2m $$. It means that in an undirected graph, there are 2m degrees for all vertices. Because for each edge, it connects two vertices so it provides 2 degrees in total.

For an directed graph: $$ \sum_{v\in V} in_deg(v) = m =  \sum_{v\in V} out_deg(v) $$.

### Representation of Graph

Two ways: Adjacency matrix and Adjacent list.

Adjacency matrix is an n*n matrix where i, j entry contains 1 if edge connects i and j or 0 if no edge.

Adjacency list: It lists all nodes in one column and following the nodes which are their neighbors. 

The complexity of two ways:

|                                                     | Adjacency List                           | Adjacency Matrix |
| --------------------------------------------------- | ---------------------------------------- | ---------------- |
| Space                                               | O(m) Depend on the edge                  | O(n^2)           |
| Accessing a node v/ Traversing all node             | O(1) / O(n)                              | O(1) / O(n)      |
| Accessing a edge e = (u,v)                          | O(\|$$\Gamma(u)$$\|) # of neighbors of u | O(1), M[u, v]    |
| Finding some neighbor of v                          | O(1)                                     | O(n)             |
| Traversing all edges/ vertices adjacent to a node u | O($$\Gamma(u)$$\|)                       | O(n)             |
| Traversing all edges                                | O(m)                                     | O(n^2)           |

### Application of dfs

##### finding SCC

Strongly connected components (SCCs) is a max set of nodes, any two of the nodes are reachable from each other.

Alg:

1. Run dfs on G
2. Flip G's edges to create G^T
3. Run dfs on G^T by traversing nodes in a decreasing order of finish time generated in step 1
4. The SCC of G is the trees of dfs forest of G^T

### Minimum spanning Tree

***Spanning tree:*** A spanning tree T of an undirected graph G is a subgraph that is a tree which includes all of the vertices of G with minimum possible number edges.

***Weighted graph:*** A weighted graph is a graph where a number is assigned to each edge. The weights may represent costs, length and some other things.

***Connected graph:*** For an undirected graph, if there is a path between two vertices (v and u), then v and u are connected. In a directed graph, the path connecting v and u must be in the same direction. A graph is called connected graph if any two vertices are connected.



For a spanning tree of a weighted connected graph, if the total weight is smallest among all spanning trees, then it is called minimum spanning tree.

***Minimum spanning Tree problem:*** Find an MST for the input graph

***Minimum spanning Forest problem:***  If the given graph is not necessarily connected, find MST for each connected component.

#### Kruskal's algorithm

Input: An edge-weighted (simple, undirected, connected) graph.

Output: an MST

Idea: Suppose G = (V(m), E(n)). We consider the graph as the forest with no edge, each vertex is a tree. Then order the weight of edges, start adding edge in non-decreasing order. If the new edge connect two vertices on the same current formed tree, we do not add this edge. If the edge connect two nodes belongs to two trees, we add this edge.

```
procedure kruskal (G)

T <-- \o
for each v \in V(G) do
	Define cluster C(v) <-- v // each vertex is a tree
sort edges in E(G) into non-decreasing weight order
for each edge e_i = (u,v) /in E(G) do
	if C(u) != C(v) then
		T <-- T /cup {e_i}
		merge clusters C(u) and C(v)
return T
```

##### Correctness of Kruskal

We prove that after every iteration of the second for loop, where we have examined i edges and have a partial solution built into T, called it T_i, there is a final MST T_opt which has all these edges of T_i and all other edges the T_opt has but T_i does not are in the edges we have not examined yet. i.e., $$T_i  \subseteq T_(opt) \subseteq T_i \cup {e_(i+1), e_(i+2), ... , e_m}  $$.

The base case is trivial. And once we prove it for the last iteration e_m, it implies the solution is MST.

So we now consider the induction step after we have T_i satisfying the ih and examine edge e_i+1. If we do not add e_i+1, then T_i = T_i+1. In this case, T_opt do not have e_i+1 too for sure. If we create a cycle with e_i+1, then T_opt cannot have e_i+1 too because all edges of T_i are in T_opt and e_i+1 cannot belong to T_opt.

If we add e_i+1 to T_i. There are two cases.

Case 1: T_opt contains it. So our T_i+1 is consistent with optimum solution.

Case 2: T_opt does not contain it. In this case, there must be a cycle in T_opt + e_i+1. This cycle contains at least one edge e_j that is not in T_i. e_j must be in {e_i+1, ... , e_m}. The reason is if e_j is in T_i, we will not add e_i+1 and in this case, e_j can only be in the remaining case we have not tested. To form a cycle, e_i+1 must be different from e_j, so j >= i+2. So w(e_j) >= w(e_i+1). So T_opt - e_j + e_i+1 is also a MST.

##### Running time

Each cluster contains the unordered linked list of vertices. Each vertex keeps the index which cluster it belongs to. At first, there are n clusters. To merge two clusters, we need to change the indexes of each vertex in the smaller cluster. So the merge step costs O(min{|C(u)|, |C(v)|}) time. 

After merging two clusters, the size of the total is at least double larger than the original smaller cluster. So for each vertex, we need at most log(n) time to finish its merge and in total, there are at most nlog(n) time for merge of all vertices. 

For the sort part, it costs O(m*log(m)) and m <= n(n-1) for an undirected graph. So O(m*log(m)) = O(mlog(n^2)) = O(2mlog(n)) = O(mlog(n)). So the total time is O((m+n)log(n)).

#### Prim's algorithm

Idea: Initialize the set V_new = {x}. x is any vertex in the set V and seen as the start vertex. E_new = {}. Repeat the following steps until V_new = V. Find the smallest weight edge in E, the edge must have a vertex u which is in V_new and a vertex v which is not in V_new. Add v into V_new and add (u, v) into E_new. Return the V_new and E_new.

```
procedure primMST(G) // G = (V, E)
S = {s}
A = empty set
while (|S| < |V|) do
	find a minimum weight edge e = (u,v), u \in S and v \notin S
	S = S \cup {v}
	A = A \cup {(u,v)}
return A
```

##### Correctness

A_i: The set of edges A in the algorithm  after i iterations of the while loop.

We can state the claim in the form, for any 0 <= i <= n-1, there exists T_opt such that $$A_i \subseteq T_opt \subseteq A_i \cup E \setminus  A_i$$. This similar proof cannot provide any convenience.

We need to prove, For all i from 0 to n-1, there exists MST T_opt such that A_i \subset T_opt. Notice that A_n-1 is a spanning tree of G, if we prove A_n-1 \subset T_opt, we prove A_n-1 is the MST.

Base step, Ind step, assume there is a T_opt such that A_i \subset T_opt, we need to show there is a $$T'_{opt}$$ such that $$A_i \cup \{new e\} \subset T'_{opt}$$.

If e \in $$T_{opt}$$, we are done. If $$e \notin T_{opt}$$, there must be an edge e' = (u', v') in $$T_{opt}$$ such that crosses the (S, $$\bar S$$). Clearly, w(e) <= w(e') because e' must not in A_i and until A_i, we have already looked for all smallest edges. In this case, $$e' \in T_{opt}$$, then we can remove e' and add e since e is smaller, $$T'_{opt} = T_{opt} \setminus {e'} \cup {e}$$

##### A revise of Prim's algorithm

Idea: For each node \notin S, keep track of the min edge that connects it to S. Update the information only for the neighbors of the node that is currently being added to S. Uses a priority queue Q on \bar S.

Pseudocode:

```
procedure primMST(G)
for each v \in V(G) do
	v.key = \infinity
	v.predec = NIL
s.key = 0
while (Q != emptyset) do
	u = ExtractMin(Q)
	for each v neighbor of u do
			if (v \in Q and w(u,v) < v.key) then
				v.predec = u
				decrease-key(Q,v,w(u,v))
```

 Time: ExtrachMin(Q) costs logn and while loop will iterate n times, so it costs nlog(n) in total. The second for loop costs mlogn.

##### A theorem from prim alg:

Let T be a spanning tree of G, T is a MST iff each edge is the min-edge crossing to cut it induces.

The cut is the connection edge of two separate parts. If the edge is cut, the tree becomes two trees.

#### The shortest path problem

Def of shortest path problem: find the shortest path in an edge-weighted graph connecting two vertices s and t.

Def of SSSP single source shortest path problem: Given an edge-weighted graph G and a source s, find out for each vertex v \in V(G) a shortest paths from s to v.

##### Some properties:

The sub-path optimality: If we find some shortest path from u_0 to u_k, then some path u_i to u_j is also the shortest path between u_i and u_j.

The shortest path is good if there are negative weight directed, if it is undirected the negative weight is meaningless. We assume no negative cycles.

For any u, we have d(u, u) = 0

For any u, v, we have d(u, v) = d(v, u) (if G is undirected)

For any u, v, w we have d(u, w) <= d(u, v) + d(v, w)

#### Dijkstra's SSSP algorithm

For graphs with non-negative weights, idea:

Maintains a set S of vertices for which we know the shortest path. Initially, S = {s}, at the end: S = V. By the greedy solution, we should choose the node in \bar S = V \setminus S with the minimum dist.

 

```
procedure dijkstra(G, w,s) //G = (V,E)
for each v do
	v.dist <-- /infinity
	v.predec <-- NIL
s.dist <-- 0
Build Min-priority-Queue Q on all nodes, k = dist
while (Q != empty) do
	u <-- EtractMin(Q)
	for each v neighbor of u
		if (v.dist > u.dist + w(u,v)) then
			v.dist <-- u.dist + w(u,v)
			v.predec <-- u
			decrease-key(Q, v, v.dist)
```





## Note from MATH 322

### Ways to creating subgraphs of a graph G

- deleting an edge e gives the subgraph G - e
- deleting a set F of edges (one or more) gives the subgraph G - F
- deleting a vertex v and all incident edges gives the subgraph G - v
- deleting a set S of vertices and all incident edges gives the subgraph G - S

### Ways to Contraction

If e is an edge in G, then G \ e is the graph obtained by: 1. removing e, and 2. identifying and making into new one the vertices incident with e

### Complements

If G is a simple graph, the complement \bar G is the simple graph with vertex set V(G) and where there is an edge between two vertices if and only is there is no such edge in G.

### Matrix representation - pass

### Example of graphs

#### Null graph

A null graph is a graph G with E(G) = empty (no edges).

Notation N_n: (Null graph with n vertices)

#### Complete graph

a complete graph is a simple graph where any two distinct vertices are adjacent

Notation K_n: complete graph with n vertices

In general, $$ \bar N_n = K_n$$, and \bar K_n = \bar \bar N_n = N_n.

G together with edge of \bar G is K_n.

K_n has (n*(n-1)) / 2 edges.

#### circle graph

A cycle graph is a connected graph where each vertex has degree 2. Notation: C_n.

#### Path graph

The path graph P_n = C_n - e (where e is any edge)

#### Wheel graph

The wheel graph W_n is obtained from C_(n-1) by adding one vertex that is attached by one edge to each vertex of C_(n-1)

#### Regular graph

A graph is called regular if all vertices have the same degree. (r-regular, if each vertex has degree r)

C_n: 2-regular, K_n: (n-1)-regular

#### Bipartite graph

A graph is bipartite if V(G) can be split into two sets B and W so that no two vertices of B are adjacent and no two vertices of W are adjacent.

#### Complete bipartite graph  

is a simple graph G where V(G) consists of two sets B and W such that 

- no two vertices of B or of W are adjacent

- each vertex of B is adjacent to each vertex of W

Notation K_r, s: complete bipartite graph with r black and s white vertices

#### k-cube

The k-cube is the simple graph Q_k where:

- V(Q_k) = the set of k-tuples (a_1, a_2, .. , a_k) of zeros and ones 
- two vertices are adjacent if and only if the tuples differ at exactly one place

k-cube is a bipartite graph

### Directed graph (digraphs)

A digraph G consists of:

- a finite set V(G) != empty of vertices.
- a finite family E(G) of ordered pairs of vertices, called arcs.

The underlying graph of D is the (usual) graph obtained by forgetting the order.

A digraph is simple if it has no loops or multiples arcs.

A digraph can be simple even if the underlying graph is not simple. A simple digraph can have the same underlying graph as a non-simple digraph.

A isomorphism of digraphs is an isomorphism of the underlying graphs that preserves the order.

The out-degree of a vertex y is the number of edge from y.

The in-degree of a vertex y is the number of edge to y.

Directed handshaking lemma: in a digraph, the sum of all in-degrees equals to the sum of all out-degrees.