[Useful section notes](https://canvas.harvard.edu/courses/170458/files/folder/Section%20Materials/Akshay%20%26%20Katie%20(Tue%204%3A30%20PM)?preview=26105116)

Given continuous random variable $X$

$$
CDF: F(x) = -\int_{-\infty}^x f(t) \,dt
$$
$$
PDF: f(x) = \frac{d}{dx}F(x)
$$

Note that $f(x)$ is not a probability, unlike the CMF. To get the probability:
$$
P(a < X \leq b) = F(b) - F(a) = \int_a^bf(x) \,dx
$$

Note that the probability of a continuous random variable being any given singular value is 0 (ie. $P(X=c)=0$ where $c$ is some constant).

A PDF $f$ needs to satisfy the following conditions:
- $f(x) \geq 0$
- $\int_{-\infty}^\infty f(x) \, dx = 1$


### Expectation of Continuous r.v.
$$
E(X) = \int_{-\infty}^{\infty} x f(x) \, dx
$$

$$
E(g(X)) = \int_{-\infty}^{\infty} g(x) f(x) \, dx
$$

### Location Scale Transformation
Let $X$ be a continuous random variable.
Let $Y = \sigma X + \mu$

If $X \sim \text{Unif}(a,b)$:
$Y \sim \text{Unif}(\sigma a+\mu, \sigma b + \mu)$

If $X \sim \mathcal{N}(0, 1)$
$Y \sim \mathcal{N}(\mu, \sigma^2)$

### CDF of a function of a r.v.
Let $X$ be a continuous random variable
Find $Y=g(X)$, where $g$ is some function

1. Write $F_Y(y)=P(g(X) \leq y)$
2. Rewrite event $\{g(X) \le y\}$ as $\{X \le g^{-1}(y) \}$. If $g$ is strictly decreasing, the inequality flips.
3. Find the probability of such an event using the CDF of $X$
4. Diffrentiate to get the PDF of $Y$