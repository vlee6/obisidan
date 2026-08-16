### Definition
Given algorithm $A$, input set $I$ of length $n$ array of $x$ key-value pairs, and `size` function $I \mapsto N$.
Asymptotic runtime $T_{algorithm}(n)$ :
$$T_{algorithm}(n)=\max_{x \in I \text{ : } size(x) \leq n} \# \text{ of basic operations preformed by } A \text { on } x$$

Note that we due to the inequality $size(x) \leq n$, we don't actually know the number of inputs we have, just that it's less than or equal to $n$.  For "flexibility", we also have a variant such that `size(x) = n` , giving us an exact number of inputs:
$$T^{=}_{algorithm}(n)=\max_{x \in I \text{ : } size(x) = n} \# \text{ of basic operations preformed by } A \text { on } x$$

Note that for all $n \in \mathbb{N}, T^=(n) \leq T(n)$ and are usually equal. $T$ is also a non-decreasing function such that $T(x) \geq T(y)$ whenever $x>y$.

$T(n)^=$ What do I see?
$T(n)$ What's the maximum that I see or have seen ($T(n)$ is a non-decreasing function)

### Notation
Let $f,g$ : $\mathbb{N} \mapsto \mathbb{R}^{\geq 0}$
- (Big O, upper bound) $f=O(g)$ if there exists $c>0$ such that for all $n$ large enough, $f(n) \leq c*g(n)$
- (Big omega, lower bound) $f=\Omega(g)$ if there exists $c>0$ such that for all $n$ large enough, $f(n) \geq c*g(n)$. Equivalently, $g=O(f)$
- (Theta) $f=\Theta(g)$ if $f=O(g)$ and $f=\Omega(g)$
- (Little o, strict upper bound) $f=o(g)$ if for **every** constant $c>0$, for all sufficiently large $n$, we have $f(n) \leq c*g(n)$
- (Little omega, strict lower bound) $f=\omega(g)$ is for **every** constant $c>0$, for all sufficiently large $n$, we have $f(n) \geq c* g(n)$. Equivalently $g=o(f)$

In simpler terms...
- Big O is the upper bound. Does there exist a function (when multiplied with some constant) that captures the entire runtime function?
- Big Omega is the lower bound. Does there exist a function (again, when multiplied by some constant) is **IS** captured by the entire runtime function?

We want our asymptotic functions to be as **tight** as possible, or as close to the runtime function.

### Methodology
Let $f,g$ : $\mathbb{N} \mapsto \mathbb{R}^{\geq0}$
If $L=\lim_{n \to \infty} \frac{f(n)}{g(n)}$ **exists** and $L \in \mathbb{R}^{\geq 0} \cup {\infty}$
- $f=O(g) \leftrightarrow L < \infty$ 
- $f=\Omega(g) \leftrightarrow L > 0$ 
- $f=\Theta(g) \leftrightarrow 0 < L < \infty$ 
- $f=o(g) \leftrightarrow L = 0$ 
- $f=\omega(g) \leftrightarrow L = \infty$ 

See [Hesterberg-Vadhan][[https://app.perusall.com/courses/compsci-1200-introduction-to-algorithms-and-their-limitations-274040074/_/library] 2.3 for examples of the different computation complexities of different sorting algorithms. 
