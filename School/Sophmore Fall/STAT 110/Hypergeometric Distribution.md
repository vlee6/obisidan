**Urn Story**
- Urn with $W$ white balls and $B$ black balls
- Draw $n$ balls without replacement
- Random variable $X = \text{\# of white balls in sample of } n \text{ balls}$

$$
X \sim \text{HGeom}(w,b,n)
$$
$$
P(X=k) = \frac{\binom{w}{k}\binom{b}{n-k}}{\binom{w+b}{n}}
$$
$$
\text{Support} = \{0, 1, 2, \dots, n\}
$$
$$
E(X) = \frac{nw}{w+b}
$$
$$
\text{Var}(X) = (\frac{w+b-n}{w+b-1}) \mu (1 - \frac{\mu}{n})
$$
