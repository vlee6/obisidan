### Cumulative Distribution Function
Accumulate probabilties from $-\infty$ to the value that we're looking at.
fhr$F: \mathbb{R} \rightarrow [0,1]$
$F(x)=P(X \leq x)$

You can easily convert from PDF to CDF and vice versa

Also note that:
$$\lim_{x \rightarrow -\infty} F_x(x)=0$$
$$\lim_{x \rightarrow \infty} F_x(x)=1$$
- CDFs are always right-continuous (ie. it approaches the value as it goes comes from the left side, never actually reaching the value at the right side)

### Hypergeometric Distribution
**Urn Story**
- Urn with $W$ white balls and $B$ black balls
- Draw $n$ balls without replacement
- Random variable $X = \text{\# of white balls in your sample}$

$$X \sim \text{HGeom}(w,b,n)$$

PMF:
$$
P(X=k) = \frac{\binom{w}{k}\binom{b}{n-k}}{\binom{w+b}{n}}
$$


**Elk Story**
- Say we had $N$ elk, $t$ of which are tagged
- Collect a simple random sample of size $n$
- Random variable $X = \text{\# of tagged elk in new sample}$ 
- What is the PMF of X?

$$
X \sim \text{HGeom}(t, N-t, n)
$$

Support:
- $0 \leq X \leq N$
- $0 \leq X \leq t$
- $0 \leq n-X \leq N-t$

PMF:
$$
P(X=k) = \frac{\binom{t}{k}\binom{N-t}{n-k}}{\binom{N}{n}}
$$

We use the hypergeometric distribution to find the probability of successes when sampling from a population without replacement.

### Geometric Distribution
Number of failures before 1st success with independent trials with probability $p$ of success.

PMF: $P(x-k)=q^kp \text{, where } q=1-p$
CDF: $\sum\limits_{l=0}^{\lfloor k \rfloor}(1-p)^lp$    (Note the floor on $k$ since we define a CDF for all real numbers, so we need to take out any non-integers since something like 3.5 failures = 3 failures)

### Expectation of a random variable
A weighted average of a random variable given the PMF:

$$
E(X)=\sum\limits_x P(X=x)x
$$
$$E(X)=P(X=x_1)x_1+P(X=x_2)x_2+P(X=x_3)x_3+...+P(X=x_n)x_n$$
$$\text{Where the support of } X =\{x_1, x_2, x_3, ...,x_n\}$$

- Expected value of a binomial distribution is $np$
- Expected value of a geometric distribution is $\frac{q}{p}$
- 