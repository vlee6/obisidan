An independent set $I$ of a graph $G=(V,E)$ is a set of vertices in $V$ (ie. $I \subset V$) such that no two vertices in $I$ are connected by an edge (ie. no two vertices in $I$ are neighbors). Notice that this definition means that a set of one vertex is technically an independent set.

A **maximal independent set** of a graph $G$ is the largest independent set that can be formed from $G$


### Greedy algorithm for finding independent sets
Choose some ordering of vertices. Begin with empty independent set $I$. Traverse vertices. Add vertex to independent set $I$ if the neighbors of this vertex are not already in independent set. Since this is a [[Greedy Algorithms]], there is no guarantee that $I$ is a maximal independent set.

Note:
*Specifically for the interval scheduling problem, if you order vertices by increasing end time and conduct the greedy algorithm, you do get an maximal independent set.*
