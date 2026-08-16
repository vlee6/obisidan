### Definition
Given $\Pi = (I, O, f)$, $\Gamma = (J,P,g)$
A reduction from $\Pi$ to $\Gamma$ is an algorithm to solve $\Pi$ using an "oracle" (any function/black box that on a query $y \in J$ outputs something in $g(y)$ or $\bot$ ) for $\Gamma$. 

$\Pi \leq_{T(n), q \otimes h(n)} \Gamma$
- $T(n)$ is the runtime of the reduction; essentially the runtime of $\Pi$ if we treat each oracle calls as one step. However, there can still be multiple oracle calls.
- $q$ is the number of times we query the oracle
- $h(n)$ is the largest size of input that will be fed into the oracle

Just remember:
Runtime of $\Pi$ $=$ RT of preprocessing step $+$ RT of postprocessing step $+$ RT of oracle ($\Gamma$) $\times$ # of oracle calls
Runtime of reduction ($\Pi \leq \Gamma$) $=$ RT preprocessing step $+$ RT of postprocessing step $+$ # of oracle calls

The difference: we pretend that an oracle call takes constant time when calculating the runtime of a reduction.

$A \leq B$
$B$ is harder than $A$. We can solve $A$ using a solver for $B$.
A reduces to B.