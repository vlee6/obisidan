Say we have $n$ cards. We flip over each card one by one and say the numbers 1 through $n$ as we go. What are the odds that the number we say matches the card?

Let $A_i$ be the event that on the $i$-th card, the number we say matches the card we flip. It should be easily apparent that:

$$P(A_i) = \frac{1}{n}$$

However, we want to find the probability of $A_1$ or $A_2$ or $A_3$, and so forth, since we only need one match to win the game.

Using the properties of inclusion exclusion, we get:

$$
P(\bigcup\limits^n_{i=1}A_i) = (P(A_1) + P(A_2)+...)-(P(A_1 \cap A_2) + P(A_2 \cap A_3)+...)+....+(-1^n)P(A_1 \cap A_2 \cap ... \cap A_n)
$$

$$
	P(\bigcup\limits^n_{i=1}A_i) = (-1)^i \binom{n}{i}n!-(n-j)!
$$

And via the Taylor series:
$$
P(\bigcup\limits^n_{i=1}A_i) = 1-\frac{1}{e}
$$