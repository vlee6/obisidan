All probabilities are conditional probabilties.
$$
P(A) = P(A | \text{all of the assumptions we make for the problem})
$$

Bayes' rule with extra conditioning
$$
P(A|B, E)=\frac{P(B|A, E) P(A|E)}{P(B|E)}
$$

LOTP with extra conditioning
$$P(B|E) = \sum\limits^n_{i=1}P(B|A_i,E)P(A_i|E)$$

### Conditional Independence
Say $A$ and $B$ are conditionally indepedence given $C$

$$
P(A \cap B|C) = P(A|C) P(B|C)
$$

Conditional dependence is a relationship between two or more events that are dependent when a third event occurs.

Suppose $A$ and $B$ are conditionally independent on $E$. By definition of conditional independence, given that $E$, knowing whether $A$ (or $A^c$) happened doesn't give us information on $B$:

$$
P(B|E,A^c) = P(B|E)
$$