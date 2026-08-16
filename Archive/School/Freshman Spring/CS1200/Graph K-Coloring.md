*Graph K-Coloring computational problem*
**Input:** Graph $G=(V,E)$ and natural number $k$
**Output:** A k-coloring of $G$ if it exists

A coloring maps each vertex in $V$ to a color such that no two vertices that share an edge between them have the same color. A coloring is often represented as a list of length $n$ such that each index $i$ in the list holds the color of vertex $i$.

### Greedy coloring
Create some arbitrary ordering of vertices. Color each vertex with the lowest possible color (if colors are represented by numbers) such that the resulting graph is still a valid coloring.

Since this is a [[Greedy Algorithms]], the result of the greedy coloring algorithm is not necessarily the most efficient coloring (ie. uses the least colors)

### BFS 2-coloring
Run greedy coloring on arbitrary start vertex and in the order that vertices are discovered in breath-first search. $O(n+m)$ runtime, the same runtime as BFS.

### Independent set 3-coloring
Utilizes the principle that a k-coloring of a graph $G$ is equivalent to partitioning $G$ into $k$ [[Independent Sets]], where each independent set is one color. $O(1.89^n)$ runtime.

For anything more than three coloring, just use greedy coloring