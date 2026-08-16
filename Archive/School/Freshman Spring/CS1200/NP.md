### $P_{search}$ complexity class
We can find a solution for our program in polynomial time.

### $P$ complexity class
A decision problem in $P_{search}$, ie. only has `yes` or `no` output.

### $EXP_{search}$ complexity class
We can find a solution for our program in exponential time.

### $EXP$ complexity class
A decision problem in $EXP_{search}$, ie. only has `yes` or `no` output.

### $NP_{search}$ complexity class
1. All valid outputs are verifiable in polynomial time
2. Valid output have sizes that are polynomial with respect to input size

The $NP$ complexity class is the decision equivalent.

The decision problem complexity class $P$ is a subset of $NP$ (since to to verify a decision that can be found in polynomial time, you can just check find the decision again in polynomial time), but $P_{search}$ is not a subset of $NP_{search}$ since there exists programs that may run in polynomial time, but do not have outputs bounded by polynomial length. 

It is unknown whether $NP$ is a subset of $P$ (and subsequently $NP=P$) or whether $NP_{search}$ is a subset of $P_{search}$.

$P_{search} \subseteq EXP_{search}$
$NP_{search} \subseteq EXP_{search}$

### NP-completeness
In order for computational problem $\Pi$ to be NP-complete
1. Show that $\Pi$ is in $NP_{search}$
2. Show that $\Pi$ is $NP_{search}$ hard. Show that a known NP-complete problems reduces to $\Pi$ in polynomial time. For example, showing that $SAT \leq_p \Pi$.
	- Don't forget the **runtime analysis** (proving that the reduction is in polynomial time) and **bidirectional proof** of correctness for your reduction.