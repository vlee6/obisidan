- **Sensitivity** (true positive rate) is the probability of a positive test result, conditioned on the individual truly being positive.
- **Specificity** (true negative rate) is the probability of a negative test result, conditioned on the individual truly being negative.

![[Pasted image 20260923161355.png]]
### Gambler's Ruin
2 gamblers, $A$ and $B$, series of $\$1$ bets.
Let $p=\text{the probability of } A \text{ wins a bet}$
Let $q=\text{the probability of } A \text{ loses a bet}$
Let $A$ start with $\$i$ and $B$ start with $\$N-i$

Find the probability that $A$ wins everything

Let $P_i = P(A \text{ wins everything} | A \text{ starts with \$i})$

$$P(\text{Reaching N without losing everything})=\frac{1-(q/p)^i}{1-(q/p)^N}$$

### Simpson's paradox
For events $A$, $B$, and $C$, we say that we have a Simpson's paradox if:
$$P(A|B,C) < P(A|B^c,C)$$
$$P(A|B,C^c) < P(A|B^c,C^c)$$
But
$$P(A|B) > P(A|B^c)$$

Just keep in mind how we aggregate data.

### Basic Probability Rules
With and without independence:
$$P(A \cup B)=P(A)+P(B)-P(A \cap B)$$
$$P(A \cap B) = P(A|B) \cdot P(B)$$