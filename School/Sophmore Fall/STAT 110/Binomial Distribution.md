Let random variable $X$ counter the number of sucesses in $r$ **independent** trials, each with probability $p$ of success.

$$
X \sim \text{Bin}(n,p)
$$
$$
P(X=k)=\binom{n}{k}p^k(1-p)^{n-k}
$$
$$
\text{Support} = \{0, 1, 2, \dots , n\}
$$
$$
E(X) = np
$$
$$
\text{Var}(X) = np
$$
### Adding (independent) Binomials
Given independent binomial random variables $X \sim \text{Bin}(n_1,p)$ and $Y \sim \text{Bin}(n_2,p)$:
$$
X+Y=\text{Bin}(n_1+n_2,p)
$$