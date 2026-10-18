Let $B_1, \dots, B_n$ be a partition of $S$ (each block $B_i$ is disjoint and the union of the blocks in the partition is $S$):
$$
P(A) = \sum\limits^n_{i=1}P(A|B_i)P(B_i)
$$
With extra conditioning:
$$
P(B|E) = \sum\limits^n_{i=1}P(B|A_i,E)P(A_i|E)
$$