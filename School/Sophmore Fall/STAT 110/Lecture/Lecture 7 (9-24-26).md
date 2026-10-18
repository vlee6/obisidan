### Random Variables
Intuitively, a random variable is a numerical summary of an experiement (how many heads after flipping 10 coins? even or odd number of heads after flipping 10 coins?)

Given an experiment with sample space $S$, a random variable is a function from the sample space $S$ to real numbers. A random variable maps every single outcome $s \in S$ to a real number.

A random variable $X$ assigns a numerical value $X(s)$ to each possible outcome $s$ of the experiment.

### Support
The support of a random variabl is the set of values for that random variable that are not probability zero. In other words, the support of a random variable is the set of all possible  values for that random variable. If we were flipping 10 coins and our random variable was measuring the number of heads, our support is integers from 1 to 10.

### Discrete vs. Continuous
**Discrete:** Support is a finite or countably infinite set
**Continous:** Support is an interval. RV can be any number in that interval. (ie. $(0, \infty)$ or $\mathbb{R}$)

### Probability Mass Function (PMF)
Let $X$ be a random variable with values $x$.
The PMF is a function:
$$P(X=x), \text{for all x}$$.
- Must be nonnegative
- Probabilities must sum to 1

Note that $X=x$ is an event!

Examples:
- Bernoulli Distribution, describes a random variable with two possible values. $X \sim \text{Bern}(p)$. $B^2=B$ since the square of 0 or 1 is equal to 0 or 1.
- Binomial Distribution, Let random variable $X$ counter the number of sucesses in $r$ **independent** trials, each with probability $p$ of success. $X \sim \text{Bin}(n,p)$. Formula is $P(X=x)=\binom{n}{x}p^x(1-p)^{n-x}$

PDF (Probability density function): Continuous random variable
PMF (Probability mass function): Discrete random variable

If you have two seperate independent random variables $X_1$ and $X_2$ with binomial distributions $X_1 \sim \text{binom}(n_1,p)$ and $X_2 \sim \text{binom}(n_2,p)$ with the same $p$'s, the sum of the random variables $X_1+X_2$ is also a random variable with distribution $X_1+X_2 \sim \text{binom}(n_1+n_2,p)$

### Distribution
A distribution of RV $X$ is the probabilities to all questions of the form "is $X \in A$?" (ie. "is $X=3$?").

