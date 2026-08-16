- "Graph" $\rightarrow$ Simple, undirected, unweighted
- "Digraph" $\rightarrow$ Simple, directed, unweighted.

**Simple**: no more than one edge between pair of vertices.
**Directed**: every edge has a direction.

A graph $G$ is a collection of vertices and edges. In computer science, we represent a graph through a set of vertices $V$ (of size $n$) and set of edges $E$ (of size $m$). For every edge $e$ in our graph, $E$ contains a coordinate pair of the two vertices connected by $e$. If we are modeling a directed graph, these coordinate pairs look like $(\text{From}, \text{To})$.

Edges in an undirected graph can also be represented by an adjacency list. Each index in an adjacency represents a vertex. At each index, there is an array of all of the vertices connected to that vertex/index by an edge.

**Understand the following topics**
1. [[Breadth First Search]]
2. [[Graph K-Coloring]]
3. [[Independent Sets]]
4. [[Matching]]

When it comes to traversing between vertices along edges...
**Walk:** A walk can repeat vertices.
**Path:** A path cannot repeat vertices
**Distance from vertex $a$ to vertex $b$:** Length of the shortest path from $a$ to $b$ (minimum number of edges)
