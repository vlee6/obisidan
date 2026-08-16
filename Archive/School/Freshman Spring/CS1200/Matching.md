A matching $M$ in graph $G=(V,E)$ is a subset of edges (ie. $M \subset E$) such that every vertex in $V$ is connected to at most one edge in $M$. No two edges in $M$ should share an endpoint. 

*Maximum matching computational problem:*
**Input:** A graph $G=(V,E)$
**Output:** A matching $M \in E$ in $G$ of maximum size

We often apply matching on bipartite graphs. A bipartite graph is a graph that can be separated into two independent sets, call them $V_0$ and $V_1$, such that every edge connect a vertex in $V_0$ to $V_1$.

### Alternating Walk
An alternating walk in $G$ with respect to matching $M$ is a walk consisting of vertices $v_0, v_1, ... v_\ell \in V$ such that:
- If the edge $(v_i,v_{i+1})$ is in $M$, then $(v_{i+1},v_{i+2})$ is in $E \setminus M$
- If the edge $(v_i,v_{i+1})$ is in $E \setminus M$, then $(v_{i+1},v_{i+2})$ is in $M$

Essentially, it's a walk in $G$ where the edges alternate from in the matching $M$ to not in the matching $M$.

### Augmenting path
An augmenting path is an alternating walk that has no repeat vertices and the vertices at the start and end of the walk (ie. $v_0,v_\ell$) are not matched in $M$.

### Berge's theorem
Suppose we have a graph $G=(V,E)$ and matching $M$. If and only if $M$ is not a maximum matching, Berge's theorem guarantees that there exists an augmenting path with respect to $M$.

### Algorithm to find maximum matching
Given a graph $G$, we can find a maximum matching on $G$ by repeatedly finding shortest augmented paths in $G$ with respect to $M$ between unmatched vertices $U_0 \in V_0$ and $U_1 \in V_1$.  Every augmented path grows the size of the matching $M$ by 1, and as long as $M$ is not a maximum matching, Berge's theorem guarantees that such an augmented path exists. If an augmented path cannot be found, then the maximum matching has been found.

Finding shortest alternating walks (and thus shortest augmented paths) take $O(n+m)$ time. Since we can only create up to $n$ augmented paths, the total runtime to find a maximum matching is $O(n(n+m))$. This reduces to $O(nm)$ as long as $m=\Omega(n)$.

Note that **maximal** and **maximum** matching are not interchangeable. Greedy will get to maximal. 