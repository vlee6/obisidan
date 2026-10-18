### Frequentist vs Bayesian
**Frequentist:** We repeat the experiment many times and then $P(A) \approx \frac{n_a}{n}$ where $n$ is the number of times we run the experiment and $n_a$ is the number of times $A$ occurs.

**Bayesian:** Degree of belief when we're uncertain of something.

### Independence:
Given events $A,B,C$.
$A$ and $B$ are independent if $P(A \cap B) = P(A)P(B)$

For three events:
$P(A \cap B)=P(A)P(B)$
$P(A \cap C)=P(A)P(C)$
$P(B \cap C)=P(B)P(C)$
$P(A \cap B \cap C)=P(A)P(B)P(A)$

Independence means multiplication.

If we learned that $A$ occured, it gives no information about whether $B$ occured.

Notation note:
$P(A,B,C) = P(A \cap B \cap C)$ 

### Conditional Probability

Definition of probability of $A$ given $B$

$$P(A|B) = \frac{P(A \cap B)}{P(B)}$$

Thus, $A$ and $B$ are independent, then $P(A|B)=\frac{P(A)P(B)}{P(B)}=P(A)$o

We can derive a lot of theorems from this.
- $P(A \cap B) = P(B)P(A|B)$
- $P(A \cap B) = P(A)P(B|A)$
- $P(A \cap B \cap C) = P(A)P(B|A)P(C| A\cap B)$

Note that, provided $P(B)>0$:
$$
P(A^c|B) = 1-P(A|B)
$$

**Bayes' rule**
$$
P(A|B) = \frac{P(B|A)P(A)}{P(B)}
$$

**Law of Total Probability**
Let $B_1,...,B_n$ be a partition of $S$ (each block $B_i$ is disjoint and the union of the blocks in the partition is $S$)

$$
P(A) = \sum\limits^n_{i=1}P(A|B_i)P(B_i)
$$

Imagine we split the sample space into 4 disjoint parts. Thus, we also split $A$ into disjoint pieces. Each term in the summation represents the interection of $A$ with one of the four partitions (since $P(A|B_i)P(B_i) = P(A \cap B_i)$), so summing those parts should give us the probbility of A.
![[Pasted image 20260915143431.png]]
Disjoint != Independence