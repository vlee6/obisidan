Let $X$ represent the count of a rare event.
$$
X \sim \text{Pois}(\lambda)
$$
$$
P(X=k)=\frac{e^{-\lambda}\lambda^k}{k!}
$$
$$
\text{Support} = \{0,1,2, \dots \}
$$
$$
E(X) = \lambda
$$
$$
\text{Var}(X) = \lambda
$$
### Poisson Paradigm
Let $A_1, \dots, A_n$ be $n$ events where $P(A_j)$ is low, $n$ is large, and thet $A_j$ are independent or weakly dependent.

Let
$$
X = \sum\limits_{j=1}^n I(A_j)
$$
count how many $A_j$ occur. Then $X$ is approximately distributed as $\text{Pois}(\lambda)$ with $\lambda = \sum^n_{j=1}P(A_j)$ (sum of the probabilites of all events).

### Adding Poissons
Given $X \sim \text{Pois}(\lambda)$ and $Y \sim \text{Pois}(\mu)$
$$X+Y \sim \text{Pois}(\lambda + \mu)$$

### Chicken-egg story
$N\sim\operatorname{Pois}(\lambda)$ eggs, each hatching independently with probability $p$. Given $N=n$, $X\sim\operatorname{Bin}(n,p)$. Unconditionally,
$$
X\sim\operatorname{Pois}(\lambda p),\qquad Y\sim\operatorname{Pois}(\lambda q),
$$
and $X$ and $Y$ are independent.