### Set theory
- Sample space $S$ of an experiment is all possible outcomes.
- An event $A$ is a subset of $S$ (ie. $A \subseteq S$).

- The union of events $A$ and $B$ (denoted by $A \cup B$) is the event that at least one of $A$ or $B$ occurs. 
- The intersection of events $A$ and $B$ (denoted by $A \cap B$) is the event that both $A$ or $B$ occurs. 
- The complement of event $A$ (denote by $A^C$) is the even that $A$ does not occur.

The probability of $A$ is equal to the 1 minus the probability of $A^C$
$$
P(A)=1-P(A^C)
$$
### Naive definition of probablility
$$
P_{naive}(A) = \frac{|A|}{|S|} = \frac{\text{number of outcomes favorable to } A}{\text{total number of outcomes in } S}
$$

### Multiplication rule
Suppose that I have an experiment that's broken down into two subexperiemnts, experiment $A$ and experiment $B$. There are $a$ outcomes in subexperiment $A$ and $b$ outcomes in subexperiment $B$. The total number of outcomes is $ab$.

See this illustrated by a matrix:

|         | a=0      | a=1      | a=2      |
| ------- | -------- | -------- | -------- |
| **b=0** | a=0, b=0 | a=1, b=0 | a=2, b=0 |
| **b=1** | a=0, b=1 | a=1, b=1 | a=2, b=1 |
| **b=2** | a=0, b=2 | a=1, b=2 | a=2, b=2 |
We have 9 total compound outcomes given 3 outcomes for subexperiemnt $A$ and 3 outcomes for subexperiemnt $B$

- A set with $n$ elements has $2^n$ subsets. For each element, they can either be in the subset or not in the subset.

### Binomial Coefficient
For nonnegative number $n$ and $k$ is the number of subsets of size $k$ that can be created from a set of size $n$. "n choose k" (without replacement)

For $k\leq N$
$$
\binom{n}{k}=\frac{n(n-1)...(n-k+1)}{k!}=\frac{n!}{(n-k)!k!}
$$
For $k < n$
$$
\binom{n}{k} = 0
$$

### Story Proofs
You tell a story to prove something.

### General definition of probability
Given sample space $S$
1. $P(\emptyset) =0$, $P(S) = 1$
2. If $A_1$, $A_2$, ... are disjoint events the the probability of their union $P(\bigcup\limits^{\infty}_{n=1}A_n)$ is sum of their probabilities $\sum\limits^{\infty}_{n=1}P(A_n)$.

$$
P(A)=1-P(A^C)
$$
$$
P(A \cup B) = P(A) + P(B) - P(A \cap B)
$$
