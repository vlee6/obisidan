### Definition
A computational problem is a tuple ($I,O,f$)
- $I$ is a set of (usually infinite) possible inputs, $O$ is a set of possible outputs
- $f$ for all $x$ that is in $I$, $f(x) \subset O$. `f(x)` is the set of valid outputs for $x$.

An algorithm solves the computational problem $\Pi$ if, for every input $x \in I$, it outputs some $y \in f(x)$ (and subsequently $y \in O$).

For the sorting problem:
- $I$ is the set of all arrays of (key,value) pairs with the key being real
- $O$ is the set of all (sorted) arrays of (key,value) pairs with the key being real
- $f: x \in I$, set of valid sorts of $x$